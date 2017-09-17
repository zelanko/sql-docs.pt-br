---
title: "Ao registrar um objeto de negócios personalizada | Microsoft Docs"
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
- custom business object in RDS [ADO]
- registering custom business objects in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: e9032ad8-d14c-42e3-ba13-cb5f00084a79
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: be54505545b80211ec34216a67596c32ca8ce2b2
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="registering-a-custom-business-object"></a>Ao registrar um objeto de negócios personalizada
Para iniciar com êxito um objeto de negócios personalizada (. dll ou .exe) por meio do servidor Web, ProgID do objeto comercial deve ser inserido no registro, conforme explicado neste procedimento. Esse recurso RDS protege a segurança do servidor Web, executando apenas sancionados executáveis.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!NOTE]
>  Para o MDAC 2.0 e posterior e Windows DAC, o objeto de negócios padrão [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), não é registrado por padrão durante a instalação de MDAC/Windows DAC. No entanto, se **RDSServer.DataFactory** foi registrado como seguros para execução no computador antes da instalação, a entrada do registro é mantida para a nova instalação.  
  
### <a name="to-register-a-custom-business-object"></a>Para registrar um objeto comercial personalizado:  
  
1.  Clique em **iniciar** e, em seguida, clique em **executar**.  
  
2.  Tipo **RegEdit** e clique em **Okey**.  
  
3.  No Editor do registro, navegue até o **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch** chave do registro.  
  
4.  Selecione o **ADCLaunch** chave e, em seguida, o **editar**, aponte para **novo** e clique em **chave**.  
  
5.  Digite o ProgID do objeto comercial personalizada e clique em **Enter**. Deixe o **valor** entrada em branco.



