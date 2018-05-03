---
title: Personalização de DataFactory | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 943deaa40e36ae099ca810df1c3a884fe2b937d1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="datafactory-customization"></a>Personalização do DataFactory
Remote Data Service (RDS) fornece uma maneira de realizar facilmente o acesso a dados em um sistema cliente/servidor de três camadas. Um controle de dados do cliente especifica parâmetros de cadeia de caracteres de conexão e comando para executar uma consulta em uma fonte de dados remota ou a cadeia de caracteres de conexão e [registros](../../../ado/reference/ado-api/recordset-object-ado.md) parâmetros para executar uma atualização do objeto.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Os parâmetros são passados para um programa de servidor que executa a operação de acesso a dados na fonte de dados remoto. RDS fornece um programa de servidor padrão chamado o [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto. O **RDSServer.DataFactory** objeto retorna qualquer **registros** objeto produzido por uma consulta ao cliente.  
  
 No entanto, o **RDSServer.DataFactory** é limitado à execução de consultas e atualizações. Ele não é possível executar qualquer processamento ou validação em cadeias de caracteres de conexão ou comando.  
  
 Com o ADO, você pode especificar que o **DataFactory** funcionam em conjunto com outro tipo de programa de servidor chamado um *manipulador*. O manipulador pode modificar cadeias de caracteres de comando e conexão de cliente antes de serem usadas para acessar a fonte de dados. Além disso, o manipulador pode impor os direitos de acesso, que controlam a capacidade do cliente para ler e gravar dados à fonte de dados.  
  
 Os parâmetros que o manipulador utiliza para modificar os parâmetros de cliente e direitos de acesso são especificados nas seções de um arquivo de personalização.  
  
 Os tópicos a seguir fornecem mais informações sobre como personalizar o **DataFactory** objeto.  
  
-   [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [Seção Conexão do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [Seção UserList do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [Seção Logs do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [Configurações necessárias de cliente](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [Escrevendo seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


