# Políticas de acesso baseadas em risco



[Política de Acesso Condicional baseada em risco de entrada](https://learn.microsoft.com/pt-br/entra/id-protection/concept-identity-protection-policies#sign-in-risk-based-conditional-access-policy)

[Política de Acesso Condicional baseada em risco de usuário](https://learn.microsoft.com/pt-br/entra/id-protection/concept-identity-protection-policies#user-risk-based-conditional-access-policy)

[Migrar políticas de risco de Proteção de ID para o Acesso Condicional](https://learn.microsoft.com/pt-br/entra/id-protection/concept-identity-protection-policies#migrate-id-protection-risk-policies-to-conditional-access)

[Habilitar o registro da autenticação multifator do Microsoft Entra](https://learn.microsoft.com/pt-br/entra/id-protection/concept-identity-protection-policies#microsoft-entra-multifactor-authentication-registration-policy)

[Conteúdo relacionado](https://learn.microsoft.com/pt-br/entra/id-protection/concept-identity-protection-policies#related-content)

As políticas de controle de acesso podem ser aplicadas para proteger as organizações, quando é detectado que uma entrada ou um usuário está em risco. Essas políticas são chamadas de **políticas baseadas em risco**.

O Acesso Condicional do Microsoft Entra oferece duas condições de risco alimentadas por sinais da Proteção de Microsoft Entra ID: **[Risco de entrada](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-conditions#sign-in-risk)** e **[Risco do usuário](https://learn.microsoft.com/pt-br/entra/identity/conditional-access/concept-conditional-access-conditions#user-risk)**. As organizações podem criar políticas de Acesso Condicional baseadas em risco, configurando essas duas condições de risco e escolhendo um método de controle de acesso. Durante cada entrada, a Proteção de ID envia os níveis de risco detectados para o Acesso Condicional, e as políticas baseadas em risco são aplicadas se as condições da política forem atendidas.

![Diagrama que mostra uma política de Acesso Condicional baseada em risco conceitual.](https://learn.microsoft.com/pt-br/entra/id-protection/media/concept-identity-protection-policies/risk-based-conditional-access-diagram.png)

Você pode exigir autenticação multifator quando o nível de risco de entrada for médio ou alto; os usuários só serão solicitados nesse nível.

![Diagrama que mostra uma política de Acesso Condicional baseada em risco conceitual com correção automática.](https://learn.microsoft.com/pt-br/entra/id-protection/media/concept-identity-protection-policies/risk-based-conditional-access-policy-example.png)

O exemplo anterior também demonstra um benefício principal de uma política baseada em risco: **correção automática de risco**. Quando um usuário conclui com êxito o controle de acesso necessário, como uma alteração de senha segura, o risco é corrigido. Essa sessão de entrada e a conta de usuário não estão em risco e nenhuma ação é necessária por parte do administrador.

Permitir que os usuários apliquem a correção automática usando esse processo reduzi significativamente a sobrecarga de investigação e correção de risco sobre os administradores, protegendo as organizações contra concessões de segurança. Mais informações sobre correção de risco podem ser encontradas no artigo [Corrigir riscos e desbloquear usuários](https://learn.microsoft.com/pt-br/entra/id-protection/howto-identity-protection-remediate-unblock).



## Política de Acesso Condicional baseada em risco de entrada

Durante cada entrada, o ID Protection analisa centenas de sinais em tempo real e calcula um nível de risco de entrada que representa a probabilidade de que a determinada solicitação de autenticação não esteja autorizada. Esse nível de risco é enviado para o Acesso Condicional, em que as políticas configuradas da organização são avaliadas. Os administradores podem configurar políticas de Acesso Condicional baseadas em risco de entrada, para impor controles de acesso com base no risco de entrada, incluindo requisitos como:

- Acesso bloqueado
- Permitir o acesso
- Exigir autenticação multifator

Se forem detectados riscos em uma entrada, os usuários poderão executar o controle de acesso necessário, como a autenticação multifator, para corrigir e fechar o evento de entrada suspeita, a fim de evitar ruídos desnecessários para administradores.

![Captura de tela de uma política de Acesso Condicional baseada em risco de entrada.](https://learn.microsoft.com/pt-br/entra/id-protection/media/concept-identity-protection-policies/sign-in-risk-policy.png)

 Observação

Os usuários já precisam ter se registrado na autenticação multifator do Microsoft Entra para disparar a política de risco de entrada.



## Política de Acesso Condicional baseada em risco de usuário

O ID Protection analisa sinais sobre contas de usuário e calcula uma pontuação de risco com base na probabilidade de o usuário estar comprometido. Se um usuário tiver um comportamento de entrada suspeita ou as credenciais dele tiverem sido vazadas, o ID Protection usa esses sinais para calcular o nível de risco do usuário. Os administradores podem configurar políticas de Acesso Condicional baseadas em risco de usuário, para impor controles de acesso com base no risco de usuário, incluindo requisitos como:

- Bloquear acesso.
- Permitir acesso, mas exigir uma alteração de senha segura.

Uma alteração de senha segura corrige o risco de usuário e fecha o evento de usuário suspeito para evitar ruídos desnecessários para administradores.



## Migrar políticas de risco de Proteção de ID para o Acesso Condicional

Se você tiver a **política de risco do usuário** ou a **política de risco de entrada** habilitada na Proteção de ID (anteriormente, Proteção de Identidade), deverá [migrá-las para o Acesso Condicional](https://learn.microsoft.com/pt-br/entra/id-protection/howto-identity-protection-configure-risk-policies#migrate-risk-policies-to-conditional-access).

 Aviso

As políticas de risco herdadas e configuradas no Microsoft Entra ID Protection serão desativadas em **1º de outubro de 2026**.

A configuração de políticas de risco no Acesso Condicional oferece benefícios como a capacidade de:

- Gerenciamento de políticas de acesso em um único local.
- Usar o modo somente relatório e as APIs do Graph.
- Aplicar a frequência de entrada para exigir reautenticação todas as vezes.
- Fornecer controle de acesso granular combinando risco com outras condições, como localização.
- Aprimorar a segurança com várias políticas baseadas em risco direcionadas a diferentes grupos de usuários ou níveis de risco.
- Aprimore a experiência de diagnóstico detalhando qual política baseada em risco foi aplicada nos Logs de entrada.
- Suporte ao sistema de autenticação de backup.



## Habilitar o registro da autenticação multifator do Microsoft Entra

O ID Protection ajuda as organizações a implantar a autenticação multifator do Microsoft Entra usando uma política que requer um registro para entrar. Habilitar essa política é uma ótima maneira de garantir que novos usuários da organização registrem para MFA no primeiro dia. A autenticação multifator é um dos métodos de autocorreção para eventos de risco no ID Protection. A autocorreção permite que os usuários tomem providências por conta própria para reduzir o volume de chamadas para assistência técnica.

Veja mais informações sobre a autenticação multifator do Microsoft Entra no artigo [Como funciona: autenticação multifator do Microsoft Entra](https://learn.microsoft.com/pt-br/entra/identity/authentication/concept-mfa-howitworks).



## Conteúdo relacionado

- [Habilitar a política de registro de autenticação multifator Microsoft Entra](https://learn.microsoft.com/pt-br/entra/id-protection/howto-identity-protection-configure-mfa-policy)
- [Habilitar as políticas de risco com usuários e entradas](https://learn.microsoft.com/pt-br/entra/id-protection/howto-identity-protection-configure-risk-policies)