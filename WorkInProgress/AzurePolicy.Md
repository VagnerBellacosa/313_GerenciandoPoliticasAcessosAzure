# O que é o Azure Policy?





[Visão geral](https://learn.microsoft.com/pt-br/azure/governance/policy/overview#overview)

[Introdução](https://learn.microsoft.com/pt-br/azure/governance/policy/overview#getting-started)

[Objetos do Azure Policy](https://learn.microsoft.com/pt-br/azure/governance/policy/overview#azure-policy-objects)

[Contagem máxima de objetos do Azure Policy](https://learn.microsoft.com/pt-br/azure/governance/policy/overview#maximum-count-of-azure-policy-objects)

[Próximas etapas](https://learn.microsoft.com/pt-br/azure/governance/policy/overview#next-steps)

O Azure Policy ajuda a impor padrões organizacionais e a avaliar a conformidade em escala. Por meio do painel de conformidade, ele fornece uma exibição agregada para avaliar o estado geral do ambiente, com a capacidade de drill down para a granularidade por recurso, por política. Ele também ajuda a deixar seus recursos em conformidade por meio da correção em massa de recursos existentes e da correção automática para novos recursos.

 Observação

Para saber mais sobre a correção, veja [Correção de recursos não compatíveis com o Azure Policy](https://learn.microsoft.com/pt-br/azure/governance/policy/how-to/remediate-resources).

Casos de uso comuns do Azure Policy incluem implementar a governança para consistência de recursos, conformidade regulatória, segurança, custo e gerenciamento. As definições de política para esses casos de uso comuns já estão disponíveis em seu ambiente do Azure como itens interno para ajudar você a começar a usar.

Especificamente, algumas ações úteis de governança que você pode impor com o Azure Policy incluem:

- Garantir que a equipe implante recursos do Azure apenas em regiões permitidas
- Impor a aplicação consistente de marcas taxonômicas
- Exigir que os recursos enviem logs de diagnóstico a um workspace do Log Analytics

É importante reconhecer que, com a introdução do [Azure Arc](https://learn.microsoft.com/pt-br/azure/azure-arc/overview), você pode estender a governança baseada em políticas para diferentes provedores de nuvem e até mesmo para os datacenters locais.

Todos os dados e objetos do Azure Policy são criptografados em repouso. Para obter mais informações, confira [Criptografia de dados em repouso do Azure](https://learn.microsoft.com/pt-br/azure/security/fundamentals/encryption-atrest).



## Visão geral

O Azure Policy avalia os recursos e as ações no Azure comparando as propriedades desses recursos com as regras de negócios. Essas regras de negócio, descritas em [Formato JSON](https://learn.microsoft.com/pt-br/azure/governance/policy/concepts/definition-structure), são conhecidas como [definições de política](https://learn.microsoft.com/pt-br/azure/governance/policy/overview#policy-definition). Para simplificar o gerenciamento, várias regras de negócio podem ser agrupadas para formar uma [iniciativa de política](https://learn.microsoft.com/pt-br/azure/governance/policy/overview#initiative-definition) (às vezes chamada de *policySet*). Depois que as regras de negócios tiverem sido formadas, a definição ou a iniciativa da política será [atribuída](https://learn.microsoft.com/pt-br/azure/governance/policy/overview#assignments) a qualquer escopo de recursos compatível com o Azure, como [grupos de gerenciamento](https://learn.microsoft.com/pt-br/azure/governance/management-groups/overview), assinaturas, [grupos de recursos](https://learn.microsoft.com/pt-br/azure/azure-resource-manager/management/overview#resource-groups) ou recursos individuais. A atribuição se aplica a todos os recursos dentro do [escopo do Resource Manager](https://learn.microsoft.com/pt-br/azure/azure-resource-manager/management/overview#understand-scope) dessa atribuição. Os subescopos podem ser excluídos, se necessário. Para obter mais informações, confira [Escopo no Azure Policy](https://learn.microsoft.com/pt-br/azure/governance/policy/concepts/scope).

O Azure Policy usa um [formato JSON](https://learn.microsoft.com/pt-br/azure/governance/policy/concepts/definition-structure) para formar a lógica que a avaliação usa para determinar se um recurso está em conformidade. As definições incluem metadados e a regra de política. A regra definida pode usar funções, parâmetros, operadores lógicos, condições e [aliases](https://learn.microsoft.com/pt-br/azure/governance/policy/concepts/definition-structure#aliases) de propriedade para corresponder exatamente ao cenário desejado. A regra de política determina quais recursos no escopo da atribuição são avaliados.



### Entender os resultados da avaliação

Os recursos são avaliados em momentos específicos durante o ciclo de vida do recurso, o ciclo de vida de atribuição de política e para avaliação regular de conformidade contínua. A seguir estão os horários ou eventos que causam a avaliação de um recurso:

- Um recurso é criado ou atualizado em um escopo com uma atribuição de política.
- Uma política ou iniciativa foi recentemente atribuída a um escopo.
- Uma política ou iniciativa já atribuída a um escopo foi atualizada.
- Durante o ciclo de avaliação de conformidade padrão, que ocorre uma vez a cada 24 horas.

Para obter informações detalhadas sobre quando e como a avaliação de política ocorre, confira [Gatilhos de avaliação](https://learn.microsoft.com/pt-br/azure/governance/policy/how-to/get-compliance-data#evaluation-triggers).



### Controlar a resposta a uma avaliação

As regras de negócio para lidar com recursos sem conformidade variam muito entre as organizações. Exemplos de como uma organização deseja que a plataforma responda a um recurso sem conformidade, incluindo:

- Negar a alteração do recurso
- Registrar a alteração no recurso
- Alterar o recurso antes da alteração
- Alterar o recurso após a alteração
- Implantar recursos em conformidade relacionados
- Bloquear ações em recursos

O Azure Policy torna cada uma dessas respostas de negócios possível por meio da aplicação de [efeitos](https://learn.microsoft.com/pt-br/azure/governance/policy/concepts/effects). Os efeitos são definidos na parte de **regra de política** da [definição de política](https://learn.microsoft.com/pt-br/azure/governance/policy/concepts/definition-structure).



### Corrigir recursos sem conformidade

Embora esses efeitos afetem um recurso principalmente quando o recurso é criado ou atualizado, o Azure Policy também é compatível com lidar com recursos que não estão em conformidade existentes sem a necessidade de alterá-los. Para obter mais informações sobre como deixar os recursos existentes em conformidade, confira [como corrigir recursos](https://learn.microsoft.com/pt-br/azure/governance/policy/how-to/remediate-resources).



### Visão geral em vídeo

A visão geral do Azure Policy a seguir é da versão 2018. Para download de vídeo ou slides, visite [Reger seu ambiente do Azure com o Azure Policy](https://learn.microsoft.com/pt-br/events/Build/2018/THR2030) no Channel 9.

<iframe src="https://www.youtube-nocookie.com/embed/dxMaYF2GB7o" frameborder="0" allowfullscreen="true" data-linktype="external" title="Vídeo: dxMaYF2GB7o" style="box-sizing: inherit; outline-color: inherit; margin: 0px; padding: 0px; border: 0px; width: 640px; height: 360px; inset: 0px;"></iframe>



## Introdução



### Azure Policy e Azure RBAC

Há algumas diferenças importantes entre o Azure Policy e o Azure RBAC (controle de acesso baseado em função). O Azure Policy avalia o estado examinando as propriedades dos recursos que são representados no Resource Manager e as propriedades de alguns provedores de recursos. O Azure Policy garante que o estado do recurso esteja em conformidade com as regras de negócio sem levar em conta quem fez a alteração ou quem tem permissão para fazer uma alteração. O Azure Policy por meio do efeito DenyAction também podem bloquear determinadas ações em recursos. Alguns recursos do Azure Policy, como [definições de política](https://learn.microsoft.com/pt-br/azure/governance/policy/overview#policy-definition), [definições de iniciativa](https://learn.microsoft.com/pt-br/azure/governance/policy/overview#initiative-definition) e [atribuições](https://learn.microsoft.com/pt-br/azure/governance/policy/overview#assignments), ficam visíveis para todos os usuários. Esse design permite transparência para todos os usuários e serviços em relação a quais regras de política são definidas no ambiente.

O Azure RBAC concentra-se em gerenciar as [ações](https://learn.microsoft.com/pt-br/azure/role-based-access-control/resource-provider-operations) do usuário em escopos diferentes. Se o controle de uma ação for necessário com base em informações do usuário, o Azure RBAC será a ferramenta correta a ser usada. Mesmo que um indivíduo tenha acesso para executar uma ação, se o resultado for um recurso que não está em conformidade, o Azure Policy ainda bloqueará a criação ou a atualização.

A combinação do RBAC do Azure e do Azure Policy fornece controle de escopo completo no Azure.



### Permissões do Azure RBAC no Azure Policy

O Azure Policy tem várias permissões, conhecidas como operações, em dois provedores de recursos:

- [Microsoft.Authorization](https://learn.microsoft.com/pt-br/azure/role-based-access-control/resource-provider-operations#microsoftauthorization)
- [Microsoft.PolicyInsights](https://learn.microsoft.com/pt-br/azure/role-based-access-control/resource-provider-operations#microsoftpolicyinsights)

Muitas funções internas concedem permissão a recursos do Azure Policy. A função **Colaborador da Política de Recursos** inclui a maioria das operações do Azure Policy. O **proprietário** tem direitos totais. Tanto o **Colaborador** quanto o **Leitor** têm acesso a todas as operações de *ler* do Azure Policy.

O **colaborador** pode disparar a correção de recursos, mas não pode *criar* ou *atualizar* definições nem atribuições. O **Administrador de Acesso do Usuário** é necessário para conceder a identidade gerenciada nas permissões necessárias de atribuições **deployIfNotExists** ou **modify**.

 Observação

Todos os objetos de Política, incluindo definições, iniciativas e atribuições, serão legíveis para todas as funções em seu escopo. Por exemplo, uma atribuição de política com escopo para uma assinatura do Azure será legível por todos os titulares de função no escopo da assinatura e abaixo.

Se nenhuma das funções internas tem as permissões necessárias, crie uma [função personalizada](https://learn.microsoft.com/pt-br/azure/role-based-access-control/custom-roles).

As operações do Azure Policy podem ter um impacto significativo no ambiente do Azure. Somente o conjunto mínimo de permissões necessárias para executar uma tarefa deve ser atribuído e essas permissões não devem ser concedidas a usuários que não precisam delas.

 Observação

A identidade gerenciada de uma atribuição de política **deployIfNotExists** ou **modify** precisa de permissões suficientes para criar ou atualizar os recursos direcionados. Para saber mais, confira [Configurar as definições de política para correção](https://learn.microsoft.com/pt-br/azure/governance/policy/how-to/remediate-resources#configure-the-policy-definition).



### Requisito de permissões especiais para o Azure Policy com o Gerenciador de Rede Virtual do Azure

O [Gerenciador de Rede Virtual do Azure (versão prévia)](https://learn.microsoft.com/pt-br/azure/virtual-network-manager/overview) permite aplicar políticas de segurança e gerenciamento consistentes a várias VNets (redes virtuais) do Azure em toda a infraestrutura de nuvem. Os grupos dinâmicos do AVNM (Gerenciador de Rede Virtual do Azure) usam as definições do Azure Policy para avaliar as respectivas associações de VNets.

Para criar, editar ou excluir políticas de grupo dinâmico do Gerenciador de Rede Virtual do Azure, você precisa:

- Ler e gravar permissões do Azure RBAC na política subjacente
- Permissões do Azure RBAC para ingressar no grupo de rede (não há suporte para autorização clássica de administrador).

Especificamente, a permissão de provedor de recursos necessária é `Microsoft.Network/networkManagers/networkGroups/join/action`.

 Importante

Para modificar os grupos dinâmicos do VNM, você deve ter acesso somente por meio da atribuição de função RBAC do Azure. Não há suporte para autorização clássica de administrador/herdada; isso significa que, se sua conta fosse atribuída apenas à função de assinatura de coadministrador, você não teria permissões em grupos dinâmicos do AVNM.



### Recursos cobertos pelo Azure Policy

Embora uma política possa ser atribuída no nível do grupo de gerenciamento, *somente* os recursos no nível da assinatura ou do grupo de recursos são avaliados.

Para determinados provedores de recursos, como [configuração de computador](https://learn.microsoft.com/pt-br/azure/governance/machine-configuration/overview), [Serviço de Kubernetes do Azure](https://learn.microsoft.com/pt-br/azure/aks/intro-kubernetes) e [Azure Key Vault](https://learn.microsoft.com/pt-br/azure/key-vault/general/overview), há uma integração mais profunda para o gerenciamento de configurações e objetos. Para obter mais informações, acesse [Modos de provedor de recursos](https://learn.microsoft.com/pt-br/azure/governance/policy/concepts/definition-structure#resource-provider-modes).



### Recomendações para o gerenciamento de políticas

Aqui estão alguns ponteiros e dicas para ter em mente:

- Comece com um efeito `audit` ou `auditIfNotExist` em vez de um efeito de imposição (`deny`, `modify` e `deployIfNotExist`) para acompanhar o impacto da definição de política nos recursos do ambiente. Se você já tiver scripts em vigor para dimensionamento automático de aplicativos, a configuração de um efeito de imposição poderá atrapalhar as tarefas de automação desse tipo que já estejam em vigor.
- É importante manter em mente as hierarquias organizacionais ao criar definições e atribuições. É recomendável criar definições em nível de assinatura ou em níveis superiores, tais como o grupo de gerenciamento. Em seguida, crie a atribuição do próximo nível filho. Se você criar uma definição de um grupo de gerenciamento, a atribuição poderá ser definida para uma assinatura ou grupo de recursos nesse grupo de gerenciamento.
- Recomendamos a criação e a atribuição de definições de iniciativa, mesmo se começar com uma única definição de política. Isso permite que você adicione definições de política à iniciativa posteriormente sem aumentar o número de atribuições a serem gerenciadas.
  - Por exemplo, imagine que você crie a definição de política *policyDefA* e a adicione à definição de iniciativa *initiativeDefC*. Se, posteriormente, você criar outra definição de política *policyDefB* com metas semelhantes a *policyDefA*, poderá adicioná-la a *initiativeDefC* e rastreá-las em conjunto.
  - Depois de criar uma atribuição de iniciativa, definições de política adicionadas à iniciativa também se tornam parte dessas atribuições de iniciativas.
  - Quando uma atribuição de iniciativa é avaliada, todas as políticas de dentro da iniciativa também são avaliadas. Se for necessário executar uma política individualmente, é melhor não incluí-la em uma iniciativa.
- Gerencie o Azure Policy como código com revisões manuais sobre alterações em definições de política, iniciativas e atribuições. Para saber mais sobre padrões sugeridos e ferramentas, consulte [Projetar o Azure Policy como fluxos de trabalho de código](https://learn.microsoft.com/pt-br/azure/governance/policy/concepts/policy-as-code).



## Objetos do Azure Policy



### Definição de política

A jornada de criação e implementação de uma política no Azure Policy começa com a criação de uma definição de política. Cada definição de política tem condições sob as quais ela é imposta. E ela tem um efeito definido que ocorre se as condições são atendidas.

No Azure Policy, oferecemos algumas políticas internas que estão disponíveis para você por padrão. Por exemplo:

- **SKUs de Conta de Armazenamento Permitidas** (Negar): Determina se uma conta de armazenamento que está sendo implantada está dentro de um conjunto de tamanhos de SKU. Seu efeito é negar todas as contas de armazenamento que não estão de acordo com o conjunto de tamanhos de SKU definido.
- **Tipo de Recurso Permitido** (Negar): Define os tipos de recursos que você pode implantar. Seu efeito é negar a todos os recursos que não fazem parte dessa lista definida.
- **Locais permitidos** (Negar): Restringe os locais disponíveis para novos recursos. O efeito é usado para impor seus requisitos de conformidade de área geográfica.
- **SKUs de Máquinas Virtuais Permitidas** (Negar): Especifica um conjunto de SKUs de máquina virtual que você pode implantar.
- **Adicionar uma marca aos recursos** (Modificar): Aplica uma tag necessária e seu valor padrão se ele não é especificado pela solicitação de implantação.
- **Não são tipos de recurso permitidos** (Negar): Impede que uma lista de tipos de recurso seja implantada.

Para implementar essas definições de política (definições internas e personalizadas), é necessário atribuí-las. Você pode atribuir qualquer uma dessas políticas usando o portal do Azure, o PowerShell ou a CLI do Azure.

A avaliação da política ocorre com diversas ações diferentes, tais como atribuição de política ou atualizações de política. Para obter uma lista completa, confira [Gatilhos de avaliação de política](https://learn.microsoft.com/pt-br/azure/governance/policy/how-to/get-compliance-data#evaluation-triggers).

Para saber mais sobre as estruturas das definições de políticas, consulte [Estrutura da definição de política](https://learn.microsoft.com/pt-br/azure/governance/policy/concepts/definition-structure).

Parâmetros de política ajudam a simplificar o gerenciamento de política, reduzindo o número de definições de política que você precisa criar. Você pode definir parâmetros ao criar uma definição de política para torná-la mais genérica. Então você pode reutilizar essa definição de política para cenários diferentes. Faça isso passando valores diferentes ao atribuir a definição de política. Por exemplo, especificar um conjunto de locais para uma assinatura.

Parâmetros são definidos durante a criação de uma definição de política. Quando um parâmetro é definido, ele recebe um nome e, opcionalmente, um valor. Por exemplo, é possível definir um parâmetro para uma política intitulada *local*. Em seguida, você poderá atribuir valores diferentes, como *EastUS* ou *WestUS* ao atribuir uma política.

Para obter mais informações sobre parâmetros de política, confira [Estrutura de definição – parâmetros](https://learn.microsoft.com/pt-br/azure/governance/policy/concepts/definition-structure#parameters).



### Definição de iniciativa

Uma definição de iniciativa é uma coleção de definições de política que são adaptadas para atingirem uma só meta abrangente. Definições de iniciativa simplificam o gerenciamento e a atribuição de definições da política. Elas simplificam agrupando um conjunto de políticas como um único item. Por exemplo, você pode criar uma iniciativa intitulada **Habilitar o monitoramento no Microsoft Defender para Nuvem.**, com uma meta para monitorar todas as recomendações de segurança disponíveis na instância do Microsoft Defender para Nuvem.

 Observação

O SDK, como a CLI do Azure e o Azure PowerShell, usa propriedades e parâmetros chamados **PolicySet** para se referir a iniciativas.

Com essa iniciativa, você teria definições de política como:

- **Monitorar um banco de dados SQL não criptografado no Microsoft Defender para Nuvem**: para o monitoramento de servidores e bancos de dados SQL não criptografados.
- **Monitorar as vulnerabilidades do sistema operacional no Microsoft Defender para Nuvem**: para o monitoramento de servidores que não satisfazem à linha de base configurada.
- **Monitorar um Endpoint Protection ausente no Microsoft Defender para Nuvem**: para o monitoramento de servidores sem um agente do Endpoint Protection instalado.

Assim como parâmetros de política, os parâmetros de iniciativa ajudam a simplificar o gerenciamento iniciativa reduzindo a redundância. Parâmetros de iniciativa são parâmetros que estão sendo usados pelas definições de política dentro da iniciativa.

Por exemplo, veja um cenário em que você tem uma definição de iniciativa, **initiativeC**, com as definições de política **policyA** e **policyB**, cada um esperando um tipo de parâmetro diferente:

Expandir a tabela

| Política | Nome do parâmetro     | Tipo do parâmetro | Observação                                                   |
| :------- | :-------------------- | :---------------- | :----------------------------------------------------------- |
| policyA  | allowedLocations      | matriz            | Esse parâmetro espera uma lista de cadeias de caracteres para um valor, pois o tipo de parâmetro foi definido como uma matriz |
| policyB  | allowedSingleLocation | string            | Esse parâmetro espera uma palavra para um valor, pois o tipo de parâmetro foi definido como uma cadeia de caracteres |

Nesse cenário, ao definir os parâmetros de iniciativa para **initiativeC**, você tem três opções:

- Use os parâmetros das definições de política contidas nessa iniciativa: Neste exemplo, *allowedLocations* e *allowedSingleLocation* tornam-se parâmetros de iniciativa para **initiativeC**.
- Forneça valores para os parâmetros das definições de política dessa definição de iniciativa. Neste exemplo, você pode fornecer uma lista de localizações para o parâmetro da **policyA** (**allowedLocations**) e o parâmetro da **policyB** (**allowedSingleLocation**). Você também pode fornecer valores ao atribuir essa iniciativa.
- Forneça uma lista de opções de *valor* que podem ser usadas ao atribuir essa iniciativa. Ao atribuir essa iniciativa, os parâmetros herdados das definições de política dentro da iniciativa só poderão ter valores dessa lista fornecida.

Ao criar opções de valor em uma definição de iniciativa, você não consegue inserir um valor diferente durante a atribuição da iniciativa, porque ele não é parte da lista.

Para saber mais sobre as estruturas de definições de iniciativa, examine [Estrutura de definição de iniciativa](https://learn.microsoft.com/pt-br/azure/governance/policy/concepts/initiative-definition-structure).



### Atribuições

Uma atribuição é uma definição ou iniciativa de política que foi atribuída para um escopo específico. Esse escopo pode variar de um [grupo de gerenciamento](https://learn.microsoft.com/pt-br/azure/governance/management-groups/overview) a um recurso individual. O termo *escopo* se refere a todos os recursos, grupos de recursos, assinaturas ou grupos de gerenciamento aos quais a definição está atribuída. As atribuições são herdadas por todos os recursos filho. Esse design significa que se uma definição for aplicada a um grupo de recursos, ela será aplicada a todos os recursos desse grupo de recursos. No entanto, você pode excluir um subescopo da atribuição.

Por exemplo, no escopo da assinatura, você pode atribuir uma definição que impede a criação de recursos de rede. Você poderia excluir um grupo de recursos dentro dessa assinatura que se destina à infraestrutura de rede. Depois, você permite acesso a esse grupo de recursos de rede a usuários em que você confia para criar recursos de rede.

Em outro exemplo, o ideal é atribuir uma definição de lista de permitidos de tipo de recurso no nível do grupo de gerenciamento. Então você atribui uma política mais permissiva (permitindo mais tipos de recurso) em um grupo de gerenciamento filho ou até mesmo diretamente em assinaturas. No entanto, este exemplo não funcionaria, pois o Azure Policy é um sistema de negação explícito. Em vez disso, você precisa excluir o grupo de gerenciamento filho ou a assinatura da atribuição no nível do grupo de gerenciamento. Depois, atribua a definição mais permissiva no grupo de gerenciamento filho ou no nível da assinatura. Se qualquer atribuição resultar na negação de um recurso, a única maneira de permitir o recurso será modificar a atribuição de negação.

As atribuições de política sempre usam o estado mais recente de sua definição ou iniciativa atribuída ao avaliar recursos. Se uma definição de política já atribuída for alterada, todas as atribuições existentes dessa definição usarão a lógica atualizada ao avaliar.

Para obter mais informações sobre como configurar atribuições de política por meio do portal, consulte [Criar uma atribuição de política para identificar recursos que não estão em conformidade em seu ambiente do Azure](https://learn.microsoft.com/pt-br/azure/governance/policy/assign-policy-portal). Etapas para o [PowerShell](https://learn.microsoft.com/pt-br/azure/governance/policy/assign-policy-powershell) e [CLI do Azure](https://learn.microsoft.com/pt-br/azure/governance/policy/assign-policy-azurecli) também estão disponíveis. Para obter informações sobre a estrutura de atribuição, confira [Estrutura de atribuições](https://learn.microsoft.com/pt-br/azure/governance/policy/concepts/assignment-structure).



## Contagem máxima de objetos do Azure Policy

Há uma contagem máxima para cada tipo de objeto do Azure Policy. Para as definições, uma entrada de *Escopo* significa o [grupo de gerenciamento](https://learn.microsoft.com/pt-br/azure/governance/management-groups/overview) ou a assinatura. Para as atribuições e isenções, uma entrada de *Escopo* significa o grupo de gerenciamento, a assinatura, o grupo de recursos ou um recurso individual.

Expandir a tabela

| Where                                                        | O que                                 | Contagem máxima |
| :----------------------------------------------------------- | :------------------------------------ | :-------------- |
| Escopo                                                       | Definições de política                | 500             |
| Escopo                                                       | Definições de iniciativa              | 200             |
| Locatário                                                    | Definições de iniciativa              | 2\.500          |
| Escopo                                                       | Atribuições de iniciativa ou política | 200             |
| Escopo                                                       | Isenções                              | 1000            |
| Definição de política                                        | Parâmetros                            | 20              |
| Definição de iniciativa                                      | Políticas                             | 1000            |
| Definição de iniciativa                                      | Parâmetros                            | 400             |
| Atribuições de iniciativa ou política                        | Exclusões (notScopes)                 | 400             |
| Regra de política                                            | Condicionais aninhadas                | 512             |
| Tarefa de correção                                           | Recursos                              | 50.000          |
| Corpo da solicitação de atribuição, iniciativa ou definição de política | Bytes                                 | 1\.048.576      |

As regras de política têm mais limites para o número de condições e a complexidade delas. Para obter mais informações, acesse os [Limites de regra de política](https://learn.microsoft.com/pt-br/azure/governance/policy/concepts/definition-structure-policy-rule#policy-rule-limits) para obter mais detalhes.



## Próximas etapas

Agora que você tem uma visão geral do Azure Policy e de alguns dos principais conceitos, aqui estão as próximas etapas sugeridas:

- [Examine a estrutura de definição de política](https://learn.microsoft.com/pt-br/azure/governance/policy/concepts/definition-structure).
- [Atribuir uma definição de política usando o portal](https://learn.microsoft.com/pt-br/azure/governance/policy/assign-policy-portal).