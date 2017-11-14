---
title: Configurando DataFactory para modos de seguros ou irrestritos | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 745f6c7408f72ee1df0c5757007588b76fe334fc
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="configuring-datafactory-for-safe-or-unrestricted-modes"></a>Configurando DataFactory para modos de seguros ou irrestritos
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Por padrão, o ADO é instalado com um "safe" [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) configuração. Modo de segurança para os componentes de servidor RDS significa o seguinte for verdadeiro:  
  
1.  Manipulador é necessário com o RDSServer.DataFactory (Isso é exigido por uma configuração de chave do registro).  
  
2.  O manipulador padrão, msdfmap.handler, estiver registrado, presente na lista de manipulador seguro e marcada como o manipulador padrão.  
  
3.  Arquivo Msdfmap.ini é instalado no diretório do Windows. Você deve configurar esse arquivo de acordo com suas necessidades, antes de usar RDS no modo de três camadas.  
  
 Opcionalmente, você pode configurar um irrestrito **DataFactory** instalação. **DataFactory** podem ser usados diretamente sem o manipulador personalizado. Os usuários ainda podem usar um manipulador personalizado ao modificar as cadeias de caracteres de conexão, mas não é necessário. Para obter mais informações sobre as implicações de usar o **RDSServer.DataFactory** de objeto, consulte [Protegendo aplicativos de RDS](../../../ado/guide/remote-data-service/securing-rds-applications.md).  
  
 O Handsafe do arquivo de registro foi fornecido para configurar as entradas de registro do manipulador para uma configuração de segurança. Para executar no modo de segurança, execute Handsafe.  
  
 Depois de executar Handsafe, você deve parar e reiniciar o serviço de publicação na World Wide Web no servidor Web, digitando os seguintes comandos em uma janela de Prompt de comando: "NET STOP W3SVC" e "NET iniciar W3SVC".  
  
## <a name="see-also"></a>Consulte também  
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)




