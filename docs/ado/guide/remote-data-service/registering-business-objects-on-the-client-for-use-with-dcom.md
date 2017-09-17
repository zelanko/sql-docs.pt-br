---
title: "Registro de objetos de negócios no cliente para uso com DCOM | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 75a21910-607f-463a-ae18-a17130dafb7e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e293eb58053259dd229656152094763ac31b48a2
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="registering-business-objects-on-the-client-for-use-with-dcom"></a>Registro de objetos de negócios no cliente para uso com DCOM
Objetos de negócios personalizada precisam garantir que o do lado do cliente pode mapear seu nome de programa (ProgId) para um identificador (CLSID) que pode ser usado ao DCOM. Por esse motivo, o ProgID do objeto DCOM deve estar no registro do cliente e mapear para a ID de classe do objeto comercial do lado do servidor. Para outros protocolos suportados (HTTP, HTTPS e em processo), isso não é necessário.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Por exemplo, se você expõe um objeto de negócios no servidor chamado MyBObj com uma ID de classe específica, por exemplo, "{00112233-4455-6677-8899-00AABBCCDDEE}", certifique-se de que as entradas a seguir são adicionadas ao registro do cliente:  
  
```  
[HKEY_CLASSES_ROOT]  
\MyBObj\Clsid\(Default) "{00112233-4455-6677-8899-00AABBCCDDEE}"  
```



