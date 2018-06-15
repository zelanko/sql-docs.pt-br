---
title: Preparando comandos | Microsoft Docs
description: Preparando comandos usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- prepared statements [OLE DB Driver for SQL Server]
- commands [OLE DB]
- command preparation [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: ca162d2fffd23b55d53d34d32ad92a5cdbce7545
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2018
ms.locfileid: "35666056"
---
# <a name="preparing-commands"></a>Preparando comandos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver OLE DB para SQL Server dá suporte à preparação de comando para otimização de várias execuções de um único comando. No entanto, o comando gera sobrecarga e um consumidor não precisará preparar um comando para executá-lo mais de uma vez. Em geral, um comando deverá ser preparado se for executado mais de três vezes.  
  
 Por razões de desempenho, a preparação é adiada até que o comando seja executado. Esse é o comportamento padrão. Não são conhecidos erros no comando que está sendo preparada até que ele seja executado ou uma operação de metapropriedade seja executada. Definir a propriedade SSPROP_DEFERPREPARE do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como FALSE pode desativar esse comportamento padrão.  
  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], quando um comando é executado diretamente (sem prepará-lo primeiro), um plano de execução é criado e armazenado em cache. Caso a instrução SQL seja executada novamente, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conta com um algoritmo eficiente que compara a nova instrução com o plano de execução existente no cache e reutiliza o plano nessa instrução.  
  
 Em comandos preparados, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece suporte nativo à preparação e à execução das instruções de comando. Quando você prepara uma instrução, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cria um plano de execução, o armazena em cache e retorna um identificador desse plano para o provedor. Em seguida, o provedor usa esse identificador para executar a instrução repetidamente. Não é criado nenhum procedimento armazenado. Como o identificador aponta diretamente o plano de execução de uma instrução SQL, e não a correspondência entre a instrução e o plano de execução no cache (como acontece com a execução direta), é mais eficiente preparar uma instrução do que executá-la diretamente, caso você saiba que ela será executada mais de uma vez.  
  
 No [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], as instruções preparadas não podem ser usadas para criar objetos temporários e referenciar procedimentos armazenados do sistema que criam objetos temporários, como tabelas temporárias. Esses procedimentos devem ser executados diretamente.  
  
 Alguns comandos jamais devem ser preparados. Por exemplo, os comandos que especificam a execução de procedimento armazenado ou incluem texto tendo em vista a criação do procedimento armazenado do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] jamais devem ser preparados.  
  
 Se um procedimento armazenado temporário é criado, o Driver OLE DB para SQL Server executa o procedimento armazenado temporário, retornando resultados como se a própria instrução foi executada.  
  
 Criação do procedimento armazenado temporário é controlada pelo Driver OLE DB para SQL Server-SSPROP_INIT_USEPROCFORPREP de propriedade de inicialização específica. Se o valor da propriedade for SSPROPVAL_USEPROCFORPREP_ON ou SSPROPVAL_USEPROCFORPREP_ON_DROP, o Driver OLE DB para SQL Server tenta criar um procedimento armazenado quando um comando está preparado. A criação do procedimento armazenado tem êxito caso o usuário do aplicativo tenha permissões suficientes no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Para os consumidores que não costumam desconectar, criação de procedimentos armazenados temporários pode exigir recursos significativos de **tempdb**, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados do sistema no qual os objetos temporários são criados. Quando o valor de SSPROP_INIT_USEPROCFORPREP é sspropval_useprocforprep _ ON, os procedimentos armazenados temporários criados pelo Driver OLE DB para SQL Server são removidos somente quando a sessão que criou o comando perde sua conexão com a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Caso essa conexão seja a padrão criada na inicialização da fonte de dados, o procedimento armazenado temporário só é descartado quando a fonte de dados deixa de ser inicializada.  
  
 Quando o valor de SSPROP_INIT_USEPROCFORPREP é SSPROPVAL_USEPROCFORPREP_ON_DROP, os procedimentos de OLE DB Driver para SQL Server temporários armazenados são descartados quando ocorre um dos seguintes:  
  
-   O consumidor usa **ICommandText:: SetCommandText** para indicar um novo comando.  
  
-   O consumidor usa **icommandprepare:: Unprepare** para indicar que deixou de exigir o texto do comando.  
  
-   O consumidor libera todas as referências ao objeto de comando que usa o procedimento armazenado temporário.  
  
 Um objeto de comando tem no máximo um procedimento armazenado temporário em **tempdb**. Qualquer procedimento armazenado temporário existente representa o texto de comando atual de um objeto de comando específico.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
