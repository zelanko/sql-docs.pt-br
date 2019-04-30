---
title: Configurando o DataFactory para modos seguros ou irrestritos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32b87f7ddcd871748adbba66eb0a64a10204f0c1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63214848"
---
# <a name="configuring-datafactory-for-safe-or-unrestricted-modes"></a>Configurar o DataFactory para modos seguros ou irrestritos
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Por padrão, o ADO é instalado com um "seguro" [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) configuração. Modo de segurança para os componentes de servidor RDS significa a seguir forem verdadeiras:  
  
1.  Manipulador é necessário com o RDSServer.DataFactory (Isso é exigido por uma configuração de chave do registro).  
  
2.  O manipulador padrão, msdfmap.handler, é registrado, presente na lista de manipulador de safe e marcada como o manipulador padrão.  
  
3.  Arquivo de Msdfmap.ini é instalado no diretório do Windows. Você deve configurar esse arquivo de acordo com suas necessidades, antes de usar RDS no modo de três camadas.  
  
 Opcionalmente, você pode configurar um irrestrito **DataFactory** instalação. **DataFactory** podem ser usados diretamente, sem o manipulador personalizado. Os usuários ainda podem usar um manipulador personalizado, modificando as cadeias de caracteres de conexão, mas não é necessária. Para obter mais informações sobre as implicações de usar o **RDSServer.DataFactory** do objeto, consulte [Protegendo aplicativos de RDS](../../../ado/guide/remote-data-service/securing-rds-applications.md).  
  
 O Handsafe do arquivo de registro foi fornecido para configurar as entradas do registro do manipulador para uma configuração de segurança. Para executar no modo de segurança, execute Handsafe.  
  
 Depois de executar Handsafe, você deve parar e reiniciar o serviço de publicação na World Wide Web no servidor Web digitando os seguintes comandos em uma janela de Prompt de comando: "NET STOP W3SVC" e "NET iniciar W3SVC".  
  
## <a name="see-also"></a>Consulte também  
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)



