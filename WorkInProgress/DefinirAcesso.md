# Definir uma política de acesso armazenada

[Criar ou modificar uma política de acesso armazenada](https://learn.microsoft.com/pt-br/rest/api/storageservices/define-stored-access-policy#create-or-modify-a-stored-access-policy)

[Modificar ou revogar uma política de acesso armazenada](https://learn.microsoft.com/pt-br/rest/api/storageservices/define-stored-access-policy#modify-or-revoke-a-stored-access-policy)

[Confira também](https://learn.microsoft.com/pt-br/rest/api/storageservices/define-stored-access-policy#see-also)

Uma política de acesso armazenado fornece um nível adicional de controle sobre SASs (assinaturas de acesso compartilhado) no nível de serviço no lado do servidor. Estabelecer uma política de acesso armazenada serve para agrupar assinaturas de acesso compartilhado e fornecer restrições adicionais para assinaturas que são associadas pela política.

Você pode usar uma política de acesso armazenada para alterar a hora de início, a hora de expiração ou as permissões de uma assinatura. Você também pode usar uma política de acesso armazenada para revogar uma assinatura após a sua emissão.

Os seguintes recursos de armazenamento oferecem suporte às políticas de acesso armazenadas:

- Contêineres de blobs
- Compartilhamentos de arquivo
- Filas
- Tabelas

 Observação

Uma política de acesso armazenada em um contêiner pode ser associada a uma assinatura de acesso compartilhado que concede permissões ao próprio contêiner ou aos blobs que ele contém. Da mesma forma, uma política de acesso armazenada em um compartilhamento de arquivos pode ser associada a uma assinatura de acesso compartilhado que concede permissões ao próprio compartilhamento ou aos arquivos que ele contém.

As políticas de acesso armazenadas não têm suporte para a SAS de delegação do usuário ou a SAS de conta.



## Criar ou modificar uma política de acesso armazenada

A política de acesso para uma assinatura de acesso compartilhado consiste na hora de início, no tempo de expiração e nas permissões para a assinatura. Você pode especificar uma das seguintes opções ou combiná-las:

- Todos esses parâmetros no URI de assinatura e nenhum na política de acesso armazenada
- Todos esses parâmetros na política de acesso armazenada e nenhum no URI

No entanto, você não pode especificar um parâmetro no token SAS e na política de acesso armazenada.

Para criar ou modificar uma política de acesso armazenada, chame a operação `Set ACL` para o recurso (confira [Definir ACL de Contêiner](https://learn.microsoft.com/pt-br/rest/api/storageservices/set-container-acl), [Definir ACL de Fila](https://learn.microsoft.com/pt-br/rest/api/storageservices/set-queue-acl), [Definir ACL de Tabela](https://learn.microsoft.com/pt-br/rest/api/storageservices/set-table-acl) ou [Definir ACL de Compartilhamento](https://learn.microsoft.com/pt-br/rest/api/storageservices/set-share-acl)) com um corpo de solicitação que especifica os termos da política de acesso. O corpo da solicitação inclui um identificador assinado exclusivo de sua escolha, com até 64 caracteres de comprimento. O corpo da solicitação também inclui parâmetros opcionais da política de acesso, da seguinte maneira:

XML

```xml
<?xml version="1.0" encoding="utf-8"?>  
<SignedIdentifiers>  
  <SignedIdentifier>
    <Id>unique-64-char-value</Id>  
    <AccessPolicy>  
      <Start>start-time</Start>  
      <Expiry>expiry-time</Expiry>  
      <Permission>abbreviated-permission-list</Permission>  
    </AccessPolicy>  
  </SignedIdentifier>  
</SignedIdentifiers>  
```

Você pode definir no máximo cinco políticas de acesso em um contêiner, tabela, fila ou compartilhamento por vez. Cada campo `SignedIdentifier`, com seu campo `Id` exclusivo, corresponde a uma política de acesso. Tentar definir mais de cinco políticas de acesso ao mesmo tempo faz com que o serviço retorne status código 400 (Solicitação Incorreta).

 Observação

Quando você cria ou atualiza uma política de acesso armazenada em um contêiner, tabela, fila ou compartilhamento, a alteração pode levar até 30 segundos para entrar em vigor. Durante esse intervalo, as solicitações em relação a uma assinatura de acesso compartilhado associada à política de acesso armazenada podem falhar com status código 403 (Proibido), até que a política de acesso fique ativa.

Você não pode especificar restrições de intervalo para entidades de tabela (`startpk`, `startrk`, `endpk`e `endrk`) em uma política de acesso armazenada.



## Modificar ou revogar uma política de acesso armazenada

Para modificar os parâmetros de uma política de acesso armazenada, você pode chamar a operação acl (lista de controle de acesso) para o tipo de recurso para substituir a política existente. Nessa operação, especifique uma nova hora de início, hora de expiração ou conjunto de permissões.

Por exemplo, se a política existente conceder permissões de leitura e gravação a um recurso, será possível modificá-la para conceder permissões somente de leitura em todas as solicitações futuras. Nesse caso, o identificador assinado da nova política, conforme especificado pelo `ID` campo , seria idêntico ao identificador assinado da política que você está substituindo.

Para revogar uma política de acesso armazenada, você pode excluí-la, renomeá-la alterando o identificador assinado ou alterar a hora de expiração para um valor no passado. A alteração do identificador assinado interrompe as associações entre todas as assinaturas existentes e a política de acesso armazenada. A alteração da hora de expiração para um valor no passado faz com que todas as assinaturas associadas expirem. A exclusão ou modificação da política de acesso armazenada afeta imediatamente todas as assinaturas de acesso compartilhadas associadas a ela.

Para remover uma única política de acesso, chame a operação do `Set ACL` recurso. Passe o conjunto de identificadores assinados que você deseja manter no contêiner. Para remover todas as políticas de acesso dos recursos, chame a operação `Set ACL` com um corpo de solicitação vazio.



## Confira também

- [Delegar acesso usando uma assinatura de acesso compartilhado](https://learn.microsoft.com/pt-br/rest/api/storageservices/delegate-access-with-shared-access-signature)
- [Conceder acesso limitado aos recursos do Armazenamento do Azure usando assinaturas de acesso compartilhado](https://learn.microsoft.com/pt-br/azure/storage/common/storage-sas-overview)