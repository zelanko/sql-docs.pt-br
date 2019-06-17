---
title: Seção de Logs do arquivo de personalização | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: d5d64dc151fbd54da17a65e2178b7f38eb6b2834
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699659"
---
# <a name="customization-file-logs-section"></a>Seção Logs do arquivo de personalização
O **logs** seção contém uma entrada de arquivo de log, que especifica o nome de um arquivo que registra erros durante a operação do **DataFactory**.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
 Uma entrada de arquivo de log está no formato:  
  
```console
  
err=  
FileName  
  
```  
  
## <a name="remarks"></a>Comentários  
  
|Parte|Descrição|  
|----------|-----------------|  
|**err**|Uma cadeia de caracteres literal que indica que essa é uma entrada de arquivo de log.|  
|*FileName*|Um nome de arquivo e caminho completo. É o nome de arquivo típico **c:\msdfmap.log**.|  
  
 O arquivo de log conterá o nome de usuário, o HRESULT, a data e a hora de cada erro.  
  
## <a name="see-also"></a>Consulte também  
 [Seção conexão do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Seção de UserList do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações de cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escrevendo seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


