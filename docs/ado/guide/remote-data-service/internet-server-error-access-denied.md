---
title: 'Erro de servidor de Internet: Acesso negado | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d7932d5d30964e654f86138a02977a27521569b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681514"
---
# <a name="internet-server-error-access-denied"></a>Erro de servidor da Internet: acesso negado
Se você receber esse erro, isso normalmente significa que o Microsoft Internet Information Services (IIS) retornou o status a seguir:  
  
 HTTP_STATUS_DENIED 401  
  
 Verifique se os diretórios acessados pelo IIS tem as permissões apropriadas. RDS podem se comunicar com um servidor Web IIS em execução em qualquer um dos três modos de autenticação de senha: anônimo, básico ou desafio/resposta do NT (chamado de autenticação do Windows integrada no Windows 2000). Além disso, o servidor Web deve ter permissões para o computador de origem de dados se ele for um computador com Windows NT/Windows 2000.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)




