# Construindo uma política de acesso condicional

[Atribuições](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-policies#assignments)

[Controles de acesso](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-policies#access-controls)

[Políticas simples](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-policies#simple-policies)

[Conteúdo relacionado](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-policies#related-content)

Conforme explicado no artigo [o que é acesso condicional](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/overview), uma política de acesso condicional é uma instrução if-then, de **atribuições** e **controles de acesso**. Uma política de acesso condicional reúne sinais para tomar decisões e impor políticas organizacionais.

Como uma organização cria essas políticas? O que é necessário? Como eles são aplicados?

[![Diagrama mostrando o conceito de sinais de Acesso Condicional e a decisão de aplicar a política organizacional.](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/media/common-conditional-access-media/conditional-access-signal-decision-enforcement.png)](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/media/common-conditional-access-media/conditional-access-signal-decision-enforcement.png#lightbox)

Várias políticas de Acesso Condicional podem se aplicar a um usuário individual a qualquer momento. Nesse caso, todas as políticas que se aplicam devem ser atendidas. Por exemplo, se uma política solicitar a autenticação multifator e outra solicitar um dispositivo em conformidade, concluía a MFA e use um dispositivo em conformidade. Todas as atribuições são avaliadas com **AND** lógicos. Se você tiver mais de uma atribuição configurada, todas as atribuições deverão ser atendidas para disparar uma política.

Se uma política em que "Exigir um dos controles selecionados" estiver selecionada, solicitaremos na ordem definida e, assim que os requisitos de política forem atendidos, o acesso será concedido.

Todas as políticas são impostas em duas fases:

- Fase 1

  : coletar detalhes da sessão

  - Colete detalhes da sessão, como o local de rede e a identidade do dispositivo, que serão necessários para a avaliação da política.
  - A fase 1 da avaliação de política ocorre para políticas e políticas habilitadas no [modo somente de relatório](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-report-only).

- Fase 2

  : imposição

  - Use os detalhes da sessão coletados na fase 1 para identificar os requisitos que não forem atendidos.
  - Se houver uma política configurada com o controle de concessão com **bloqueio**, a implementação irá parar nesse ponto e o usuário será bloqueado.
  - O usuário será solicitado a cumprir mais requisitos de controle de concessão que não foram atendidos durante a fase 1 na seguinte ordem, até que a política seja satisfeita:
    1. [Autenticação multifator](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-grant#require-multifactor-authentication)
    2. [Dispositivo ser marcado como em conformidade](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-grant#require-device-to-be-marked-as-compliant)
    3. [Dispositivo ingressado no Microsoft Entra híbrido](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-grant#require-hybrid-azure-ad-joined-device)
    4. [Aplicativo do cliente aprovado](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-grant#require-approved-client-app)
    5. [Política de proteção do aplicativo](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-grant#require-app-protection-policy)
    6. [Alteração de senha](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-grant#require-password-change)
    7. [Termos de uso](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-grant#terms-of-use)
    8. [Controles personalizados](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-grant#custom-controls-preview)
  - Após todos os controles de concessão serem satisfeitos, aplique os controles de sessão (Implementado por Aplicativo, Microsoft Defender para Aplicativos de Nuvem e Tempo de Vida do token)
  - A fase 2 da avaliação de política ocorre para todas as políticas habilitadas.



## Atribuições

A parte de atribuições controla quem, e onde a política de Acesso Condicional.



### Usuários e grupos

Os [Usuários e grupos](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-users-groups) atribuem quem a política irá incluir ou excluir ao ser aplicada. Essa atribuição pode incluir todos os usuários, grupos específicos de usuários, funções de diretório ou usuários convidados externos.





### Recursos de destino

Os [Recursos de Destino](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-cloud-apps) podem incluir ou excluir aplicativos de nuvem, ações de usuário ou contextos de autenticação que estão sujeitos à política.





### Rede

A [Rede](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-assignment-network) contém endereços IP, regiões geográficas e a [rede em conformidade com o Acesso Seguro Global](https://learn.microsoft.com/pt-br/entra/global-secure-access/how-to-compliant-network) para as decisões de política do Acesso Condicional. Os administradores podem optar por definir locais e marcar alguns deles como confiáveis para os locais de rede principais de suas organizações.



### Condições

Uma política pode conter várias [condições](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-conditions).



#### Risco de entrada

Para organizações com [Microsoft Entra ID Protection](https://learn.microsoft.com/pt-br/entra/id-protection/overview-identity-protection), as detecções de risco geradas podem influenciar suas políticas de acesso condicional.



#### Plataformas de dispositivo

As organizações com várias plataformas de sistemas operacionais de dispositivos podem querer implementar políticas específicas nas diferentes plataformas.

As informações usadas para calcular a plataforma de dispositivo vêm de fontes não verificadas, como cadeias de caracteres de agente do usuário que podem ser alteradas.



#### Aplicativos cliente

O software que o usuário está usando para acessar o aplicativo na nuvem. Por exemplo, "Navegador" e "Clientes de aplicativos móveis e de desktop". Por padrão, todas as políticas de Acesso Condicional recém-criadas serão aplicadas a todos os tipos de aplicativos clientes, mesmo que a condição dos aplicativos clientes não esteja configurada.



#### Filtro para dispositivos

Esse controle permite direcionar dispositivos específicos com base em seus atributos para uma política.



## Controles de acesso

A parte controles de acesso da política de acesso condicional controla como uma política é imposta.



### Conceder

[Grant](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-grant) fornece aos administradores um meio de imposição de política onde eles podem bloquear ou conceder acesso.



#### Bloquear acesso

Bloquear o acesso faz exatamente isso: bloqueia o acesso no âmbito das atribuições especificadas. O controle de bloco é poderoso e deve ser atraente com o conhecimento apropriado.



#### Permitir acesso

O controle de concessão pode disparar a imposição de um ou mais controles.

- Exigir autenticação multifator
- Exigir que o dispositivo seja marcado como em conformidade (Intune)
- Exigir um dispositivo ingressado no Microsoft Entra híbrido
- Exigir um aplicativo cliente aprovado
- Exigir uma política de proteção de aplicativo
- Exigir alteração de senha
- Requerer termos de uso

Os administradores podem optar por exigir um dos controles anteriores ou todos os controles selecionados usando as opções a seguir. O padrão para vários controles é exigir todos.

- Exigir todos os controles selecionados (controle e controle)
- Exigir um dos controles selecionados (controle ou controle)



### Session

Os [controles de sessão](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-session) podem limitar a experiência dos usuários.

- Usar restrições de aplicativo implementadas:
  - Atualmente, funciona somente com o Exchange Online e o SharePoint Online.
  - Passa informações do dispositivo para permitir o controle da experiência que concede acesso completo ou limitado.
- Usar o Controle de Aplicativos de Acesso Condicional:
  - Usa sinais do Microsoft Defender for Cloud Apps a fim de fazer coisas como:
    - Bloquear download, cortar, copiar e imprimir documentos confidenciais.
    - Monitore o comportamento de sessão arriscada.
    - Exigir rotulagem de arquivos confidenciais.
- Frequência de login:
  - Capacidade de alterar a frequência de entrada padrão para autenticação moderna.
- Sessão persistente do navegador:
  - Permite que os usuários permaneçam conectados depois de fechar e reabrir a janela do navegador.
- Personalizar a avaliação contínua de acesso
- Desabilitar padrões de resiliência



## Políticas simples

Uma política de acesso condicional deve conter, no mínimo, o seguinte para ser aplicado:

- **Nome** da política.
- Atribuições
  - **Usuários e/ou grupos** aos quais aplicar a política.
  - **Aplicativos de nuvem ou ações** às quais aplicar a política.
- Controles de acesso
  - **Conceder** ou **Bloquear** controles

![Limpar política de Acesso Condicional](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/media/concept-conditional-access-policies/conditional-access-blank-policy.png)

O artigo [políticas de acesso condicional comum](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-policy-common) inclui algumas políticas que achamos que seriam úteis para a maioria das organizações.



## Conteúdo relacionado

- [Criar uma política de Acesso Condicional](https://learn.microsoft.com/pt-br/entra/identity/authentication/tutorial-enable-azure-mfa?bc=/azure/active-directory/conditional-access/breadcrumb/toc.json&toc=/azure/active-directory/conditional-access/toc.json#create-a-conditional-access-policy)
- [Gerenciando a conformidade do dispositivo com o Intune](https://learn.microsoft.com/pt-br/mem/intune/protect/device-compliance-get-started)
- [Microsoft Defender for Cloud Apps e Acesso Condicional](https://learn.microsoft.com/pt-br/defender-cloud-apps/proxy-intro-aad)