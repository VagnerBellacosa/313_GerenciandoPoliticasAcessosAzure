# Estrutura e políticas de Acesso Condicional

[Convenções de nomenclatura](https://learn.microsoft.com/pt-br/azure/architecture/guide/security/conditional-access-framework#naming-conventions)

[Esquema de numeração](https://learn.microsoft.com/pt-br/azure/architecture/guide/security/conditional-access-framework#numbering-scheme)

[Tipos de política](https://learn.microsoft.com/pt-br/azure/architecture/guide/security/conditional-access-framework#policy-types)

[Apl](https://learn.microsoft.com/pt-br/azure/architecture/guide/security/conditional-access-framework#app)

Este artigo fornece uma estrutura para implementar uma arquitetura de Acesso Condicional baseada em persona, como a descrita na [arquitetura de Confiança Zero de Acesso Condicional](https://learn.microsoft.com/pt-br/azure/architecture/guide/security/conditional-access-architecture). Neste artigo, há detalhes sobre como formar e nomear as políticas de Acesso Condicional. Há também um ponto de partida para criar políticas.

Se você não usar uma estrutura como a fornecida aqui, incluindo um padrão de nomenclatura, as políticas tenderão a ser criadas ao longo do tempo por pessoas diferentes de maneira ad hoc. Isso pode resultar em políticas que se sobrepõem. Se a pessoa que criou uma política não estiver mais disponível, poderá ser difícil para outras pessoas saberem a finalidade da política.

Seguir uma estrutura facilita a compreensão das políticas. Ela também facilita a cobertura de todos os cenários e evita políticas conflitantes que são difíceis para solucionar problemas.



## Convenções de nomenclatura

Uma convenção de nomenclatura definida corretamente ajuda você e seus colegas a entender a finalidade de uma política, o que permite uma solução de problemas e um gerenciamento de políticas mais fácil. Sua convenção de nomenclatura deve se ajustar à estrutura que você usa para estruturar suas políticas.

A política de nomenclatura recomendada é baseada em personas, tipos de política e aplicativos. Ela tem esta aparência:

**<CANumber>-<Persona>-<PolicyType>-<App>-<Platform>-<GrantControl>-<OptionalDescription>**

Os componentes desse nome são descritos aqui:

Expandir a tabela

| Componente de nomenclatura | Descrição/Exemplo                                            |
| :------------------------- | :----------------------------------------------------------- |
| Número da AC               | Usado para identificar rapidamente o escopo e a ordem do Tipo de Política. Exemplo: CA001-CA099. |
| Persona                    | Global, Administradores, Internos, Externos, GuestUsers, GuestAdmins, Microsoft365ServiceAccounts, AzureServiceAccounts, CorpServiceAccounts. |
| Tipo de Política           | BaseProtection, AppProtection, DataProtection, IdentityProtection, AttackSurfaceReduction, Conformidade. |
| Apl                        | AllApps, O365 (para todos os serviços do Office 365), EXO (para Exchange Online). |
| Plataforma                 | AnyPlatform, Desconhecido, WindowsPhone, macOS, iOS, Android. |
| Controle de concessão      | Bloquear, ADHJ, Conformidade, Não Gerenciado (não gerenciado é especificado na condição de estado do dispositivo). |
| Descrição                  | Descrição opcional da finalidade da política.                |



## Esquema de numeração

Para facilitar a administração, sugerimos o seguinte esquema de numeração:

Expandir a tabela

| Grupo de personas               | Alocação de número |
| :------------------------------ | :----------------- |
| CA-Persona-Global               | CA001-CA099        |
| CA-Persona-Admins               | CA100-CA199        |
| CA-Persona-Internals            | CA200-CA299        |
| CA-Persona-Externals            | CA300-CA399        |
| CA-Persona-GuestUsers           | CA400-CA499        |
| CA-Persona-GuestAdmins          | CA500-CA599        |
| CA-Persona-M365ServiceAccounts  | CA600-CA699        |
| CA-Persona-AzureServiceAccounts | CA700-CA799        |
| CA-Persona-CorpServiceAccounts  | CA800-CA899        |
| CA-Persona-WorkloadIdentities   | CA900-CA999        |
| CA-Persona-Developers           | CA1000-CA1099      |



## Tipos de política

Estes são os tipos de política recomendados:

Expandir a tabela

| Tipo de política       | Descrição/exemplos                                           |
| :--------------------- | :----------------------------------------------------------- |
| BaseProtection         | Para cada persona, há uma proteção de linha de base coberta por esse tipo de política. Para usuários em dispositivos gerenciados, esse normalmente é um usuário conhecido e um dispositivo conhecido. Para convidados externos, pode ser usuário conhecido e autenticação multifator.  A proteção base é a política padrão para todos os aplicativos para usuários na persona fornecida. Se um aplicativo específico deve ter uma política diferente, exclua esse aplicativo da política de proteção base e adicione uma política explícita direcionada somente a esse aplicativo.  Exemplo: suponha que a proteção base para Internos é exigir um usuário conhecido e um dispositivo conhecido para todos os aplicativos de nuvem, mas você deseja permitir o Outlook na Web de qualquer dispositivo. Você pode excluir o Exchange Online da política de proteção base e adicionar uma política separada para Exchange Online, em que você requer autenticação multifator OU dispositivo conhecido. |
| IdentityProtection     | Além da proteção base para cada persona, você pode ter políticas de Acesso Condicional relacionadas à identidade.  Exemplos: bloquear a autenticação herdada, exigir autenticação multifator extra para alto risco de entrada ou usuário, exigir dispositivo conhecido para registro de autenticação multifator. |
| DataProtection         | Esse tipo de política indica políticas delta que protegem os dados como uma camada extra sobre a proteção base.  Exemplos:Políticas de proteção de aplicativos para iOS e Android que você pode usar para criptografar dados em um telefone e que fornecem proteção aprimorada desses dados. (As políticas de proteção de aplicativos também incluem a proteção de aplicativo.)Políticas de sessão em que a Proteção de Informações do Azure ajuda a proteger dados durante o download se os dados forem confidenciais. |
| AppProtection          | Esse tipo de política é outra adição à proteção base.  Exemplos:Suponha que você queira permitir acesso Web ao Exchange Online de qualquer dispositivo. Você pode excluir o Exchange da política base e criar uma política explícita para acesso ao Exchange, em que, por exemplo, você permite apenas o acesso somente leitura ao Exchange Online.Suponha que você exija autenticação multifator para o registro do Microsoft Endpoint Manager. Você pode excluir o registro do Intune Endpoint Manager da política base e adicionar uma política de proteção de aplicativo que exija autenticação multifator para o registro do Endpoint Manager. |
| AttackSurfaceReduction | A finalidade desse tipo de política é atenuar vários ataques.  Exemplos:Se uma tentativa de acesso vem de uma plataforma desconhecida, pode ser uma tentativa de ignorar as políticas de Acesso Condicional nas quais você precisa de uma plataforma específica. Você pode bloquear solicitações de plataformas desconhecidas para atenuar esse risco.Bloqueie o acesso aos serviços do Office 365 para Administradores do Azure ou bloqueie o acesso a um aplicativo para todos os usuários se o aplicativo for conhecido por ser ruim. |
| Conformidade           | Você pode usar uma política de conformidade para exigir que um usuário exiba os termos de uso para convidados que acessam serviços ao cliente. |



## Apl

A seguinte tabela descreve o componente Aplicativo de um nome de política:

Expandir a tabela

| Nome do aplicativo | Descrição/exemplos                                           |
| :----------------- | :----------------------------------------------------------- |
| AllApps            | AllApps indica que todos os aplicativos de nuvem são direcionados na política de Acesso Condicional. Todos os pontos de extremidade são abordados, incluindo aqueles que dão suporte ao Acesso Condicional e aqueles que não o fazem. Em alguns cenários, direcionar todos os aplicativos não funciona bem. É recomendável direcionar todos os aplicativos na política base para que todos os pontos de extremidade sejam cobertos por essa política. Novos aplicativos que aparecem no Microsoft Entra ID também irão aderir automaticamente à política. |
| <AppName>          | <AppName> é um espaço reservado para o nome de um aplicativo que a política aborda. Evite tornar o nome muito longo.  Nomes de exemplo:EXO para o Exchange OnlineSPO para o SharePoint Online |



## Tipo de plataforma

A seguinte tabela descreve o componente Plataforma de um nome de política:

Expandir a tabela

| Tipo de plataforma | Descrição                                                    |
| :----------------- | :----------------------------------------------------------- |
| AnyPlatform        | A política tem como destino qualquer plataforma. Normalmente, você configura isso selecionando **Qualquer Dispositivo**. (Nas políticas de Acesso Condicional, a *plataforma* de palavra e o *dispositivo* de palavra são usados.) |
| iOS                | A política tem como destino plataformas Apple iOS.           |
| Android            | A política tem como destino plataformas Google Android.      |
| Windows            | Essa política visa as plataformas Windows.                   |
| Linux              | Essa política visa as plataformas Linux.                     |
| WindowsPhone       | A política tem como destino plataformas Windows Phone.       |
| macOS              | A política tem como destino plataformas macOS                |
| iOSAndroid         | A política tem como destino plataformas iOS e Android.       |
| Desconhecido       | A política tem como destino qualquer plataforma não listada anteriormente. Normalmente, você configura isso incluindo **Qualquer Dispositivo** e excluindo todas as plataformas individuais. |



## Tipos de controle de concessão

A seguinte tabela descreve o componente Controle de Concessão de um nome de política:

Expandir a tabela

| Tipo de concessão     | Descrição/exemplos                                           |
| :-------------------- | :----------------------------------------------------------- |
| Bloquear              | A política bloqueia a entrada                                |
| MFA                   | A política requer a autenticação multifator.                 |
| Em conformidade       | A política requer um dispositivo em conformidade, conforme determinado pelo Endpoint Manager. Portanto, o dispositivo precisa ser gerenciado pelo Endpoint Manager. |
| CompliantorAADHJ      | A política requer um dispositivo em conformidade OU um dispositivo ingressado híbrido no Microsoft Entra. Um computador corporativo padrão ingressado no domínio também é ingressado no Microsoft Entra ID. Os celulares e computadores Windows 10 que são cogerenciados ou ingressados no Microsoft Entra podem estar em conformidade. |
| CompliantandAADHJ     | A política requer um dispositivo que esteja em conformidade E que esteja ingressado híbrido no Microsoft Entra. |
| MFAorCompliant        | A política exigirá uma autenticação multifator OU dispositivo em conformidade se ela não estiver em conformidade. |
| MFAandCompliant       | A política exige uma autenticação multifator E um dispositivo em conformidade. |
| MFAorAADHJ            | A política exigirá um computador ingressado híbrido no Microsoft Entra OU a autenticação multifator se não for um computador ingressado híbrido no Microsoft Entra. |
| MFAandAADHJ           | A política exige computador ingressado híbrido no Microsoft Entra E uma autenticação multifator. |
| RequireApprovedClient | A política requer um aplicativo cliente aprovado.            |
| AppProtection         | A política requer proteção do aplicativo                     |
| Não gerenciado        | A política visa dispositivos que não são conhecidos pelo Microsoft Entra ID. Por exemplo, você pode usar esse tipo de concessão para permitir o acesso ao Exchange Online de qualquer dispositivo. |



## Localizações nomeadas

Recomendamos que você defina esses locais padrão para uso em políticas de Acesso Condicional:

- **IPs confiáveis/redes internas.** Essas sub-redes IP representam locais e redes que têm restrições de acesso físico ou outros controles em vigor, como gerenciamento de sistema de computador, autenticação em nível de rede ou detecção de intrusão. Esses locais são mais seguros, portanto, a imposição do Acesso Condicional pode ser flexível. Considere se o Azure ou outros locais de datacenter (IPs) devem ser incluídos nesse local ou ter seus próprios locais nomeados.
- **IPs confiáveis do Citrix.** Se você tiver o Citrix local, poderá ser útil configurar endereços IPv4 de saída separados para as fazendas Citrix, se você precisar se conectar a serviços de nuvem usando sessões do Citrix. Nesse caso, você poderá excluir esses locais das políticas de Acesso Condicional, se necessário.
- **Locais do Zscaler, se aplicável.** Os computadores têm um agente ZPA instalado e encaminham todo o tráfego para a Internet para ou por meio da nuvem do Zscaler. Portanto, vale a pena definir IPs de origem do Zscaler no Acesso Condicional e exigir que todas as solicitações de dispositivos não móveis passem pelo Zscaler.
- **Países/regiões com os quais negócios são permitidos.** Pode ser útil dividir países/regiões em dois grupos de locais: um que representa áreas do mundo em que os funcionários normalmente trabalham e outro que representa outros locais. Isso permite que você aplique controles adicionais a solicitações originadas de fora das áreas em que sua organização normalmente opera.
- **Locais em que a autenticação multifator pode ser difícil ou impossível.** Em alguns cenários, a exigência de autenticação multifator pode dificultar o trabalho dos funcionários. Por exemplo, a equipe pode não ter tempo ou oportunidade para responder a desafios frequentes de autenticação multifator. Ou, em alguns locais, a triagem de RF ou a interferência elétrica podem dificultar o uso de dispositivos móveis. Normalmente, você usaria outros controles nesses locais ou eles poderiam ser confiáveis.

Os controles de acesso baseados em local dependem do IP de origem de uma solicitação para determinar o local do usuário no momento da solicitação. Não é fácil realizar falsificação na Internet pública, mas a proteção oferecida pelos limites de rede pode ser considerada menos relevante do que antes. Não recomendamos depender apenas do local como uma condição para acesso. Mas, para alguns cenários, pode ser o melhor controle que você pode usar, como se você estivesse protegendo o acesso de uma conta de serviço do local que é usado em um cenário não interativo.



## Políticas recomendadas de Acesso Condicional

Criamos uma planilha que contém políticas recomendadas de Acesso Condicional. Você pode [baixar a planilha aqui](https://github.com/microsoft/ConditionalAccessforZeroTrustResources/raw/main/ConditionalAccessSamplePolicies/Microsoft Conditional Access for Zero trust persona based policies.xlsx).

Use as políticas sugeridas como ponto de partida.

Suas políticas provavelmente mudarão ao longo do tempo para acomodar casos de uso importantes para sua empresa. Aqui estão alguns exemplos de cenários que podem exigir alterações:

- Implemente o acesso somente leitura ao Exchange Online para funcionários que usam qualquer dispositivo não gerenciado com base na autenticação multifator, na proteção do aplicativo e em um aplicativo cliente aprovado.
- Implemente a proteção de informações para garantir que as informações confidenciais não serão baixadas sem uma proteção aprimorada fornecida pelo Proteção de Informações do Azure.
- Forneça proteção contra cópia e colagem por convidados.

No momento, várias versões prévias estão entrando em visualização pública, portanto, espere atualizações para o conjunto sugerido de políticas de início de AC (Acesso Condicional) em breve.



## Diretrizes de Acesso Condicional

Agora que você tem um conjunto inicial de políticas de Acesso Condicional, você precisa implantá-las de maneira controlada e em fases. Sugerimos que você use um modelo de implantação.

Aqui está uma abordagem:

![Diagram that shows a Conditional Access deployment model.](https://learn.microsoft.com/pt-br/azure/architecture/guide/security/images/conditional-access-deployment.svg)

A ideia é primeiro implantar políticas em um pequeno número de usuários dentro de um grupo de personas. Você pode usar um grupo do Microsoft Entra associado chamado Persona Ring 0 para essa implantação. Depois de verificar se tudo funciona, você altera a atribuição para um grupo, Persona Ring 1, que tem mais membros e assim por diante.

Em seguida, habilite as políticas usando a mesma abordagem baseada em anel até que todas as políticas sejam implantadas.

Normalmente, você gerencia os membros do anel 0 e do anel 1 manualmente. Um grupo de anel 2 ou 3 que contém centenas ou até milhares de usuários pode ser gerenciado por meio de um grupo dinâmico baseado em uma porcentagem dos usuários em uma determinada persona.

O uso de anéis como parte de um modelo de implantação não é apenas para implantação inicial. Você também pode usá-lo quando novas políticas ou alterações nas políticas existentes forem necessárias.

Com uma implantação concluída, você também deve projetar e implementar os controles de monitoramento que foram [discutidos nos princípios de Acesso Condicional](https://learn.microsoft.com/pt-br/azure/architecture/guide/security/conditional-access-design#principles-of-conditional-access).

Além de automatizar a implantação inicial, convém automatizar as alterações nas políticas usando pipelines de CI/CD. Você pode usar o Microsoft365DSC para essa automação.



## Colaboradores

*Esse artigo é mantido pela Microsoft. Ele foi originalmente escrito pelos colaboradores a seguir.*

Autor principal:

- [Claus Jespersen](https://www.linkedin.com/in/claus-jespersen-25b0422/) | ID do Consultor de Entidade de Segurança&Sec

*Para ver perfis não públicos do LinkedIn, entre no LinkedIn.*



## Próximas etapas

- [Roteiro de aprendizagem: implementar e gerenciar identidade e acesso](https://learn.microsoft.com/pt-br/training/paths/implement-manage-identity-access)
- [Políticas de Acesso Condicional](https://learn.microsoft.com/pt-br/azure/active-directory/conditional-access/concept-conditional-access-policies)



## Recursos relacionados

- [Visão geral do Acesso Condicional](https://learn.microsoft.com/pt-br/azure/architecture/guide/security/conditional-access-zero-trust)
- [Princípios e dependências de design de acesso condicional](https://learn.microsoft.com/pt-br/azure/architecture/guide/security/conditional-access-design)
- [Design de Acesso Condicional baseado em Confiança Zero e personas](https://learn.microsoft.com/pt-br/azure/architecture/guide/security/conditional-access-architecture)
- [IDaaS do Microsoft Entra em operações de segurança](https://learn.microsoft.com/pt-br/azure/architecture/example-scenario/aadsec/azure-ad-security)