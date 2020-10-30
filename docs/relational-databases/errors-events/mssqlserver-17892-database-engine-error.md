---
description: MSSQLSERVER_17892
title: MSSQLSERVER_17892
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17892 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 59cf1ed10d71bf9813f2ce814d88e7f7d64b6b2e
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418650"
---
# <a name="mssqlserver_17892"></a>MSSQLSERVER_17892
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|17892|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|SRV_LOGON_FAILED_BY_TRIGGER|
|Texto da mensagem|Falha no logon para \<Login Name> devido à execução do gatilho.|
||

## <a name="explanation"></a>Explicação

O erro 17892 é gerado quando um código de gatilho de logon não pode ser executado com êxito. Os [gatilhos de logon](/sql/relational-databases/triggers/logon-triggers) acionam procedimentos armazenados em resposta a um evento LOGON. Esse evento ocorre quando é estabelecida uma sessão de usuário com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Uma mensagem de erro semelhante à seguinte é relatada ao usuário:

> Mensagem 17892, Nível 14, Estado 1, Servidor \<Server Name>, Linha 1  
Falha no logon para \<Login Name> devido à execução do gatilho.

## <a name="possible-causes"></a>Possíveis causas

O problema poderá ocorrer se houver um erro ao executar o código de gatilho para essa conta de usuário específica. Alguns dos cenários incluem:

- O gatilho tenta inserir dados em uma tabela que não existe.
- O logon não tem permissões no objeto referenciado pelo gatilho de logon.

## <a name="user-action"></a>Ação do usuário

Use uma das resoluções abaixo, dependendo do cenário.

- **Cenário 1** : No momento, você tem acesso a uma sessão aberta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma conta de administrador

  Nesse caso, você pode executar a ação corretiva necessária para corrigir o código do gatilho.

  - Exemplo 1: Se um objeto referenciado pelo código do gatilho não existir, crie esse objeto para que o gatilho de logon possa ser executado com êxito.

  - Exemplo 2: Se um objeto referenciado pelo código de gatilho existir, mas os usuários não tiverem permissões, conceda a eles os privilégios necessários para acessar o objeto.  
  
  Como alternativa, você pode apenas remover ou desabilitar o gatilho de logon, de modo que os usuários possam continuar fazendo logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

- **Cenário 2** : Você não tem nenhuma sessão atual aberta com privilégios de administrador, mas a DAC (Conexão de Administrador Dedicada) está habilitada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

    Nesse caso, você pode usar a conexão DAC para executar as mesmas etapas, conforme discutido no Caso 1, pois as conexões DAC não são afetadas pelos gatilhos de logon. Para obter mais informações sobre a conexão DAC, confira: [Conexão de diagnóstico para administradores de banco de dados](/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators).

    Para verificar se o DAC está habilitado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se há uma mensagem semelhante à seguinte:

    > 09/02/2020 16:17:44.150 Foi estabelecido suporte para conexão de administrador Dedicado do Servidor para escuta local na porta 1434.  

- **Cenário 3** : Você não tem o DAC habilitado no servidor nem tem uma sessão de administrador existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

    Nesse cenário, a única maneira de corrigir o problema é executar as seguintes etapas:
  
    1. Interrompa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os serviços relacionados.
    2. Inicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [prompt de comando](/previous-versions/sql/sql-server-2008-r2/ms180965(v=sql.105)) usando os parâmetros de inicialização `-c`, `-m` e `-f`. Essa ação desabilita o gatilho de logon e permite tomar as mesmas medidas corretivas discutidas no **Caso 1** acima.
  
        > [!NOTE]
        > O procedimento descrito acima exige uma *SA* ou uma conta de administrador equivalente.
  
         Para obter mais informações sobre essas e outras opções de inicialização, confira: [Opções de Inicialização do Serviço de Mecanismo de Banco de Dados](/sql/database-engine/configure-windows/database-engine-service-startup-options).

## <a name="more-information"></a>Mais informações

Outra situação em que ocorre uma falha nos gatilhos de logon é quando a função `EVENTDATA` é usada. Essa função retorna um XML e diferencia maiúsculas de minúsculas.  Portanto, você cria o seguinte gatilho de logon, com o intuito de bloquear o acesso baseado no endereço IP, e poderá ter este problema:

``` sql
 CREATE TRIGGER tr_logon_CheckIP  
 ON ALL SERVER  
 FOR LOGON  
 AS
 BEGIN
  IF IS_SRVROLEMEMBER ( 'sysadmin' ) = 1  
     BEGIN
         DECLARE @IP NVARCHAR ( 15 );  
         SET @IP = ( SELECT EVENTDATA ().value ( '(/EVENT_INSTANCE/ClientHost)[1]' , 'NVARCHAR(15)' ));  
         IF NOT EXISTS( SELECT IP FROM DBAWork.dbo.ValidIP WHERE IP = @IP )  
         ROLLBACK ;  
     END ;  
 END ;  
 GO
```

O usuário não manteve o uso de maiúsculas e minúsculas ao copiar este script da Internet nesta parte do gatilho:

```sql
 SELECT EVENTDATA ().value ( '(/event_instance/clienthost)[1]' , 'NVARCHAR(15)' ));  
```

Como consequência, `EVENTDATA` sempre retornava **NULL** e todos os logons de SA equivalentes tiveram o acesso negado. Nesse caso, a conexão DAC não foi habilitada e, portanto, não tínhamos escolha a não ser reiniciar o servidor com os parâmetros de inicialização listados acima para remover o gatilho.
