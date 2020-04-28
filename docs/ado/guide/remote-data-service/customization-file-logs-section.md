---
title: Seção logs de arquivo de personalização | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- logs section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: a368e264-865c-41ee-be00-d9097255c2ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14c5436478444e525c7a9753cf3e4e5cddb92f5d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922784"
---
# <a name="customization-file-logs-section"></a>Seção Logs do arquivo de personalização
A seção **logs** contém uma entrada de arquivo de log, que especifica o nome de um arquivo que registra erros durante a operação do **DataFactory**.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
 Uma entrada do arquivo de log está no formato:  
  
```console
  
err=  
FileName  
  
```  
  
## <a name="remarks"></a>Comentários  
  
|Parte|Descrição|  
|----------|-----------------|  
|**erra**|Uma cadeia de caracteres literal que indica que se trata de uma entrada de arquivo de log.|  
|*FileName*|Um caminho completo e um nome de arquivo. O nome de arquivo típico é **c:\msdfmap.log**.|  
  
 O arquivo de log conterá o nome de usuário, HRESULT, data e hora de cada erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Seção conexão de arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Seção UserList do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalização de datafactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações do cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escrever seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


