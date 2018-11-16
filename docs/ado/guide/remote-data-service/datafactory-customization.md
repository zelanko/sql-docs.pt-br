---
title: Personalização do DataFactory | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31434e08443bc533c7e2ae14ed70d6962aea04cf
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558603"
---
# <a name="datafactory-customization"></a>Personalização do DataFactory
Serviço de dados remota (RDS) fornece uma maneira de executar facilmente o acesso a dados em um sistema de três camadas de cliente/servidor. Um controle de dados do cliente especifica os parâmetros de cadeia de caracteres de conexão e comando para executar uma consulta em uma fonte de dados remota ou a cadeia de caracteres de conexão e [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) parâmetros para executar uma atualização do objeto.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Os parâmetros são passados para um programa de servidor que executa a operação de acesso a dados na fonte de dados remoto. O RDS fornece um programa de servidor padrão chamado de [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto. O **RDSServer.DataFactory** objeto retorna qualquer **Recordset** objeto produzido por uma consulta para o cliente.  
  
 No entanto, o **RDSServer.DataFactory** é limitado a executar consultas e atualizações. Ele não é possível executar nenhuma validação ou processamento em que as cadeias de caracteres de conexão ou o comando.  
  
 Com o ADO, você pode especificar que o **DataFactory** funcionam em conjunto com outro tipo de programa de servidor chamado um *manipulador*. O manipulador pode modificar cadeias de caracteres de comando e conexão de cliente antes de serem usadas para acessar a fonte de dados. Além disso, o manipulador pode impor os direitos de acesso, que controlam a capacidade do cliente para ler e gravar dados na fonte de dados.  
  
 Os parâmetros que o manipulador usa para modificar os parâmetros de cliente e direitos de acesso são especificados nas seções de um arquivo de personalização.  
  
 Os tópicos a seguir fornecem mais informações sobre como personalizar o **DataFactory** objeto.  
  
-   [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [Seção Conexão do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [Seção UserList do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [Seção Logs do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [Configurações necessárias de cliente](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [Escrevendo seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


