---
description: Personalização do DataFactory
title: Personalização de datafactory | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
author: rothja
ms.author: jroth
ms.openlocfilehash: 014341cc860e9db53447abc5db08169ba0e0b5b4
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978197"
---
# <a name="datafactory-customization"></a>Personalização do DataFactory
O RDS (serviço de dados remotos) fornece uma maneira de executar facilmente o acesso a dados em um sistema cliente/servidor de três camadas. Um controle de dados do cliente especifica parâmetros de conexão e de cadeia de caracteres de comando para executar uma consulta em uma fonte de dados remota, ou parâmetros de objeto [Recordset](../../reference/ado-api/recordset-object-ado.md) e de cadeia de conexão para executar uma atualização.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Os parâmetros são passados para um programa de servidor, que executa a operação de acesso a dados na fonte de dados remota. O RDS fornece um programa de servidor padrão chamado objeto [RDSServer. datafactory](../../reference/rds-api/datafactory-object-rdsserver.md) . O objeto **RDSServer. datafactory** retorna qualquer objeto **Recordset** produzido por uma consulta ao cliente.  
  
 No entanto, o **RDSServer. datafactory** é limitado à execução de consultas e atualizações. Ele não pode executar nenhuma validação ou processamento nas cadeias de caracteres de conexão ou de comando.  
  
 Com o ADO, você pode especificar que o **DataFactory** funcione em conjunto com outro tipo de programa de servidor chamado de *manipulador*. O manipulador pode modificar a conexão do cliente e as cadeias de caracteres de comando antes que elas sejam usadas para acessar a fonte de dados. Além disso, o manipulador pode impor direitos de acesso, que regem a capacidade do cliente de ler e gravar dados na fonte de dados.  
  
 Os parâmetros usados pelo manipulador para modificar os parâmetros de cliente e os direitos de acesso são especificados em seções de um arquivo de personalização.  
  
 Os tópicos a seguir fornecem mais informações sobre como personalizar o objeto **DataFactory** .  
  
-   [Noções básicas sobre o arquivo de personalização](./understanding-the-customization-file.md)  
  
-   [Seção Conexão do arquivo de personalização](./customization-file-connect-section.md)  
  
-   [Seção SQL do arquivo de personalização](./customization-file-sql-section.md)  
  
-   [Seção UserList do arquivo de personalização](./customization-file-userlist-section.md)  
  
-   [Seção Logs do arquivo de personalização](./customization-file-logs-section.md)  
  
-   [Configurações necessárias de cliente](./required-client-settings.md)  
  
-   [Escrever seu próprio manipulador personalizado](./writing-your-own-customized-handler.md)