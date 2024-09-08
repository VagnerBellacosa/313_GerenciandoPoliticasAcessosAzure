# O que é Acesso Condicional?

[Sinais comuns](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/overview#common-signals)

[Decisões comuns](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/overview#common-decisions)

[Políticas comumente aplicadas](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/overview#commonly-applied-policies)

[Experiência do administrador](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/overview#administrator-experience)

O perímetro de segurança moderno se estende além do perímetro de rede de uma organização para incluir a identidade do usuário e do dispositivo. As organizações agora usam esses sinais de identidade como parte de suas decisões de controle de acesso. O acesso condicional do Microsoft Entra reúne sinais para tomar decisões e impor políticas organizacionais. O Acesso Condicional é o [mecanismo de política de Confiança Zero](https://learn.microsoft.com/pt-br/security/zero-trust/deploy/identity) da Microsoft levando em conta sinais de várias fontes ao impor decisões de política.

[![Diagrama mostrando o conceito de sinais de Acesso Condicional e a decisão de aplicar a política organizacional.](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/media/common-conditional-access-media/conditional-access-signal-decision-enforcement.png)](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/media/common-conditional-access-media/conditional-access-signal-decision-enforcement.png#lightbox)

Em sua definição mais simples, as políticas de Acesso Condicional são instruções se-então, **se** um usuário quiser acessar um recurso, **então** ele deverá concluir uma ação. Por exemplo: se um usuário quiser acessar um aplicativo ou serviço como o Microsoft 365, ele deverá executar a autenticação multifator para obter acesso.

Os administradores enfrentam dois objetivos principais:

- Capacitar os usuários para serem produtivos sempre e em qualquer lugar
- Proteger os ativos da organização

Use as políticas de Acesso Condicional, para aplicar os controles de acesso certos, quando necessário, para manter sua organização segura.

 Importante

As políticas de Acesso Condicional são impostas após a conclusão do primeiro fator de autenticação. O Acesso Condicional não se destina à primeira linha de defesa de uma organização para cenários como ataques de DoS (negação de serviço), mas pode usar sinais desses eventos para determinar o acesso.



## Sinais comuns

O Acesso Condicional leva em conta sinais de várias fontes ao tomar decisões de acesso.

![Diagrama mostrando o Acesso Condicional como o mecanismo de política de Confiança Zero que agrega sinais de várias fontes.](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/media/overview/conditional-access-central-policy-engine-zero-trust.png)

Esses sinais incluem:

- Associação de usuário ou grupo
  - As políticas podem ser direcionadas a usuários e grupos específicos, proporcionando aos administradores um controle refinado sobre o acesso.
- Informações de localização de IP
  - As organizações podem criar intervalos de endereços IP confiáveis que podem ser usados ao tomar decisões sobre política.
  - Os administradores podem especificar intervalos de IP para bloquear ou permitir o tráfego proveniente de países/regiões inteiros.
- Dispositivo
  - Os usuários com dispositivos de plataformas específicas ou marcados com um estado específico podem ser usados ao impor políticas de acesso condicional.
  - Use filtros para dispositivos para direcionar políticas para dispositivos específicos, como estações de trabalho de acesso privilegiado.
- Aplicativo
  - Os usuários que tentam acessar aplicativos específicos podem disparar diferentes políticas de Acesso Condicional.
- Detecção de risco calculado e em tempo real
  - A integração do Signals ao [Microsoft Entra ID](https://learn.microsoft.com/pt-br/entra/id-protection/overview-identity-protection) permite que as políticas de acesso condicional identifiquem e corrijam usuários suspeitos e comportamentos de login.
- Microsoft Defender for Cloud Apps
  - Permite que o acesso e as sessões do aplicativo do usuário sejam monitorados e controlados em tempo real. Essa integração aumenta a visibilidade e o controle sobre o acesso às atividades realizadas em seu ambiente de nuvem.



## Decisões comuns

- Acesso bloqueado
  - Decisão mais restritiva
- Conceder acesso
  - Decisões menos restritivas podem exigir uma ou mais das seguintes opções:
    - Exigir autenticação multifator
    - Exigir força de autenticação
    - Exigir que o dispositivo seja marcado como em conformidade
    - Exigir um dispositivo ingressado no Microsoft Entra híbrido
    - Exigir um aplicativo cliente aprovado
    - Exigir uma política de proteção de aplicativo
    - Exigir alteração de senha
    - Requerer termos de uso



## Políticas comumente aplicadas

Muitas organizações têm [preocupações comuns sobre o acesso, com as quais as políticas de Acesso Condicional podem ajudar](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-policy-common), como:

- Como exigir a autenticação multifator para usuários com funções administrativas
- Como exigir a autenticação multifator para tarefas de gerenciamento do Azure
- Bloquear entradas de usuários que tentam usar protocolos de autenticação herdados
- Exigir locais confiáveis para registro de informações de segurança
- Bloquear ou permitir acesso em localizações específicas
- Bloquear comportamentos de entrada de risco
- Exigir dispositivos gerenciados pela organização para aplicativos específicos

Os administradores podem criar políticas do zero ou começar de uma política de modelo no portal ou usando o API do Microsoft Graph.



## Experiência do administrador

Os administradores com a função de [Administrador do Acesso Condicional](https://learn.microsoft.com/pt-br/entra/identity/role-based-access-control/permissions-reference#conditional-access-administrator) podem gerenciar políticas.

O Acesso Condicional é encontrado no [centro de administração do Microsoft Entra](https://entra.microsoft.com/) em **Proteção**>**Acesso Condicional**.

[![Captura de tela da página de visão geral do Acesso Condicional.](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/media/overview/conditional-access-overview.png)](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/media/overview/conditional-access-overview.png#lightbox)

- A página **Visão geral** fornece um resumo do estado da política, usuários, dispositivos e aplicativos, bem como alertas gerais e de segurança com sugestões.
- A página **Cobertura** fornece uma sinopse dos aplicativos com e sem cobertura da política de Acesso Condicional nos últimos sete dias.
- A página **Monitoramento** permite que os administradores vejam um gráficos de logins que podem ser filtrados para ver possíveis lacunas na cobertura da política.

As políticas de Acesso Condicional na página **Políticas** podem ser filtradas por administradores com base em itens como ator, recurso de destino, condição, controle aplicado, estado ou data. Essa capacidade de filtragem permite que os administradores encontrem políticas específicas com base em sua configuração rapidamente.



## Requisitos de licença

O uso desse recurso requer licenças P1 do Microsoft Entra ID. Para encontrar a licença certa para seus requisitos, confira [Comparar recursos do Microsoft Entra ID com disponibilidade geral](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

Os clientes com [licenças do Microsoft 365 Business Premium](https://learn.microsoft.com/pt-br/office365/servicedescriptions/office-365-service-descriptions-technet-library) também têm acesso aos recursos do acesso condicional.

As políticas baseadas em risco exigem acesso à [Proteção do Microsoft Entra ID](https://learn.microsoft.com/pt-br/entra/id-protection/overview-identity-protection), que exige licenças P2.

Outros produtos e recursos que interagem com políticas de Acesso Condicional exigem o licenciamento adequado para esses produtos e recursos.

Quando as licenças necessárias para o Acesso Condicional expiram, as políticas não são desabilitadas ou excluídas automaticamente. Isso concede aos clientes a capacidade de migrar das políticas de Acesso Condicional sem uma mudança repentina na sua postura de segurança. As políticas restantes podem ser exibidas e excluídas, mas não são mais atualizadas.

[Os padrões de segurança](https://learn.microsoft.com/pt-br/entra/fundamentals/security-defaults) ajudam na proteção contra ataques relacionados à identidade e estão disponíveis para todos os clientes.



## Confiança zero

Esse recurso ajuda as organizações a alinhar suas [identidades](https://learn.microsoft.com/pt-br/security/zero-trust/deploy/identity) com os três princípios orientadores de uma arquitetura de Confiança Zero:

- Verificação explícita
- Use o mínimo de privilégios
- Pressupor a violação

Para saber mais sobre a Confiança Zero e outras maneiras de alinhar sua organização aos princípios orientadores, confira o [Centro de Diretrizes da Confiança Zero](https://learn.microsoft.com/pt-br/security/zero-trust/).



## Próximas etapas

- [Como criar uma política de acesso condicional por partes](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-policies)
- [Planejar sua implantação de Acesso Condicional](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/plan-conditional-access)