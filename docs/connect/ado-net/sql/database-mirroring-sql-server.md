---
title: Espelhamento de banco de dados no SQL Server
description: Descreve a funcionalidade de espelhamento de banco de dados.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 89befaff-bb46-4290-8382-e67cdb0e3de9
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: c7ace2feb39bcc3f5f257c0ac2c7360649cfc33c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78897006"
---
# <a name="database-mirroring-in-sql-server"></a>Espelhamento de banco de dados no SQL Server

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

O espelhamento de banco de dados no SQL Server permite manter uma cópia, ou espelho, de um banco de dados do SQL Server em um servidor em espera. O espelhamento garante que haja sempre duas cópias distintas dos dados, garantindo alta disponibilidade e redundância completa dos dados. O Microsoft SqlClient Provider para SQL Server fornece suporte implícito ao espelhamento de banco de dados, de forma que, depois que ele for configurado para o banco de dados do SQL Server, o desenvolvedor não precise realizar nenhuma ação nem escrever nenhum código. Além disso, o objeto <xref:Microsoft.Data.SqlClient.SqlConnection> oferece suporte a um modo de conexão explícito que permite fornecer o nome de um servidor de parceiro de failover no <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
A sequência de eventos simplificada a seguir ocorre para um objeto <xref:Microsoft.Data.SqlClient.SqlConnection> direcionado a um banco de dados configurado para espelhamento:  
  
1. O aplicativo cliente se conecta com sucesso ao banco de dados principal, e o servidor envia de volta o nome do servidor de parceiro, que é então armazenado em cache no cliente.  
  
2. Se o servidor contendo o banco de dados principal falhar ou a conectividade for interrompida, o status da transação e da conexão será perdido. O aplicativo cliente tenta restabelecer uma conexão com o banco de dados principal e falha.  
  
3. O aplicativo cliente tenta então, de forma transparente, estabelecer uma conexão com o banco de dados espelho no servidor parceiro. Caso tenha êxito, a conexão será redirecionada ao banco de dados espelho, que, então, se tornará o novo banco de dados principal.  
  
## <a name="specifying-the-failover-partner-in-the-connection-string"></a>Especificar o parceiro de failover na cadeia de conexão  
Se você fornecer o nome de um servidor de parceiro de failover na cadeia de conexão, o cliente tentará uma conexão de forma transparente com o parceiro de failover se o banco de dados principal estiver indisponível quando o aplicativo cliente se conectar pela primeira vez.  
  
```csharp
";Failover Partner=PartnerServerName"  
```  
  
Se você omitir o nome do servidor do parceiro de failover e o banco de dados principal estiver indisponível quando o aplicativo cliente se conectar pela primeira vez, uma <xref:Microsoft.Data.SqlClient.SqlException> será gerada.  
  
Quando uma <xref:Microsoft.Data.SqlClient.SqlConnection> for aberta com êxito, o nome do parceiro de failover será retornado ao servidor e substituirá qualquer valor fornecido na cadeia de conexão.  
  
> [!NOTE]
>  Especifique, de forma explícita, o nome do banco de dados ou do catálogo inicial na cadeia de conexão para cenários de espelhamento de banco de dados. Se o cliente receber informações de failover em uma conexão que não tem um banco de dados ou um catálogo inicial explicitamente especificado, as informações de failover não serão armazenadas em cache e o aplicativo não tentará fazer o failover se o servidor principal falhar. Se uma cadeia de conexão tiver um valor para o parceiro de failover, mas nenhum valor para o banco de dados ou o catálogo inicial, uma `InvalidArgumentException` será gerada.  
  
## <a name="retrieving-the-current-server-name"></a>Recuperar o nome do servidor atual  
Em caso de failover, é possível recuperar o nome do servidor com o qual a conexão atual é realizada usando a propriedade <xref:Microsoft.Data.SqlClient.SqlConnection.DataSource%2A> de um objeto <xref:Microsoft.Data.SqlClient.SqlConnection>. O seguinte fragmento de código recupera o nome do servidor ativo, presumindo que as referências da variável de conexão são um <xref:Microsoft.Data.SqlClient.SqlConnection> aberto.  
  
Quando ocorre um evento de failover e a conexão é transferida para o servidor espelho, a propriedade **DataSource** é atualizada para refletir o nome do espelho.  
  
```csharp  
string activeServer = connection.DataSource;  
```  
  
## <a name="sqlclient-mirroring-behavior"></a>Comportamento de espelhamento do SqlClient  
O cliente sempre tenta se conectar ao servidor principal atual. Se houver falha, ele experimentará o parceiro de failover. Se o banco de dados espelho já tiver sido substituído para a função principal no servidor do parceiro, a conexão terá êxito e o novo mapeamento de espelho principal será enviado para o cliente e armazenado em cache pelo tempo de vida da chamada <xref:System.AppDomain>. Não é armazenado no repositório persistente e não está disponível para conexões subsequentes em um **AppDomain** ou processo diferente. No entanto, está disponível para conexões subsequentes dentro do mesmo **AppDomain**. Observe que outro **AppDomain** ou processo que é executado no mesmo computador ou em um computador diferente sempre tem o pool de conexões, e essas conexões não são redefinidas. Nesse caso, se o banco de dados primário falhar, cada processo ou **AppDomain** falhará uma vez, e o pool será automaticamente limpo.  
  
> [!NOTE]
>  O suporte ao espelhamento no servidor é configurado com base no banco de dados. Se operações de manipulação de dados forem executadas em relação a outros bancos de dados não inclusos no conjunto principal/espelho, seja usando nomes com várias partes ou alterando o banco de dados atual, as alterações desses outros bancos de dados não serão propagadas em caso de falhas. Nenhum erro é gerado quando os dados são modificados em um banco de dados não espelhado. O desenvolvedor deve avaliar o possível impacto das operações.  
  
## <a name="next-steps"></a>Próximas etapas
### <a name="database-mirroring-resources"></a>Recursos de espelhamento de bancos de dados  
Para obter a documentação conceitual e as informações sobre como configurar, implantar e administrar o espelhamento, consulte os seguintes recursos na documentação do SQL Server.  
  
|Recurso|DESCRIÇÃO|  
|--------------|-----------------|  
|[Espelhamento de Banco de Dados](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)|Descreve como definir e configurar o espelhamento no SQL Server.|  
