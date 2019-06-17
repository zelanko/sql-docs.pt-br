---
title: Registrando objetos de negócios no cliente para uso com DCOM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 75a21910-607f-463a-ae18-a17130dafb7e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2bbd0266dac1edc66bf70a21e51c9967af4d5fc0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699627"
---
# <a name="registering-business-objects-on-the-client-for-use-with-dcom"></a>Registrar objetos de negócios no cliente para uso com DCOM
Objetos comerciais personalizados precisam garantir que o lado do cliente pode mapear seu nome de programa (ProgId) para um CLSID (identificador) que pode ser usado ao DCOM. Por esse motivo, o ProgID do objeto DCOM deve estar no registro do lado do cliente e mapear para a ID de classe do objeto comercial do lado do servidor. Para os outros protocolos com suporte (HTTP, HTTPS e em processo), isso não é necessário.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Por exemplo, se você expõe um objeto de negócios do lado do servidor chamado MyBObj com uma ID de classe específica, por exemplo, "{00112233-4455-6677-8899-00AABBCCDDEE}", certifique-se de que as entradas a seguir são adicionadas ao registro de cliente:  
  
```console
[HKEY_CLASSES_ROOT]  
\MyBObj\Clsid\(Default) "{00112233-4455-6677-8899-00AABBCCDDEE}"  
```


