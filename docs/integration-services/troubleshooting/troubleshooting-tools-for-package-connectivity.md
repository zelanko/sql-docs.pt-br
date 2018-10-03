---
title: Ferramentas de solução de problemas para conectividade de pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- connectivity [Integration Services], troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: 08a019f5-8ba7-4527-97c1-e9846d4022ff
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0984613ed3fc299da60113c9701d30f6ccf36e74
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782904"
---
# <a name="troubleshooting-tools-for-package-connectivity"></a>Solucionando problemas de ferramentas para conectividade de pacote
O [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] contém recursos e ferramentas que você pode usar para solucionar problemas de conectividade entre pacotes e fontes de dados das quais os pacotes extraem e carregam dados.  
  
## <a name="troubleshooting-issues-with-external-data-providers"></a>Solucionando problemas com provedores de dados externos  
 Muitos pacotes falham durante as interações com os provedores de dados externos. Entretanto, as mensagens que esses provedores retornam ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] geralmente não fornecem informações suficientes para iniciar a solução de problemas da interação. Para direcionar a solução de problemas necessária, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui as mensagens de log que podem ser usadas para solucionar problemas de interação do pacote com as fontes de dados externas.  
  
-   **Habilitar os logs e selecionar o evento Diagnóstico do pacote para ver as mensagens de solução de problemas**. Os seguintes componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] são capazes de gravar uma mensagem para o log antes e após cada chamada a um provedor de dados externos:  
  
    -   Gerenciador de conexões do OLE DB, origem e destino do OLE DB  
  
    -   Gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] e origem do ADO NET  
  
    -   Tarefa Executar SQL  
  
    -   Transformações Pesquisa, Comando OLE DB e Dimensão de Alteração Lenta  
  
     As mensagens de log incluem o nome do método que está sendo chamado. Por exemplo, essas mensagens de log podem incluir o método **Open** de um objeto **Connection** OLE DB ou o método **ExecuteNonQuery** de um objeto **Command**. As mensagens têm o seguinte formato, em que '%1!s!' é um espaço reservado para as informações do método:  
  
    ```  
    ExternalRequest_pre: The object is ready to make the following external request: '%1!s!'.  
    ExternalRequest_post: '%1!s!'. The external request has completed.  
    ```  
  
     Para solucionar o problema de interação com o provedor de dados externos, analise o log para ver se cada mensagem "antes de" (`ExternalRequest_pre`) apresenta uma mensagem "depois de" (`ExternalRequest_post`) correspondente. Caso não haja uma mensagem "depois de" correspondente, significa que o provedor de dados externos não respondeu conforme o esperado.  
  
     O exemplo a seguir mostra algumas linhas de um log de exemplo que contém essas mensagens de log:  
  
    ```  
    ExternalRequest_pre: The object is ready to make the following external request: 'ITransactionJoin::JoinTransaction'.  
    ExternalRequest_post: 'ITransactionJoin::JoinTransaction succeeded'. The external request has completed.  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.Open'.  
    ExternalRequest_post: 'IDbConnection.Open succeeded'. The external request has completed.  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.CreateCommand'.  
    ExternalRequest_post: 'IDbConnection.CreateCommand finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbCommand.ExecuteReader'.  
    ExternalRequest_post: 'IDbCommand.ExecuteReader finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDataReader.GetSchemaTable'.  
    ExternalRequest_post: 'IDataReader.GetSchemaTable finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDataReader.Close'.  
    ExternalRequest_post: 'IDataReader.Close finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.Close'.  
    ExternalRequest_post: 'IDbConnection.Close finished'. The external request has completed."  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Solucionando problemas de ferramentas para desenvolvimento de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)   
 [Ferramentas de solução de problemas de execução de pacote](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
