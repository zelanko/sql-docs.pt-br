---
description: 'Erro de servidor da Internet: acesso negado'
title: 'Erro do servidor de Internet: acesso negado | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
author: rothja
ms.author: jroth
ms.openlocfilehash: d5902892fa850808afe69e0795c485ce5e46a604
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978057"
---
# <a name="internet-server-error-access-denied"></a>Erro de servidor da Internet: acesso negado
Se você receber esse erro, isso geralmente significa que o Microsoft Serviços de Informações da Internet (IIS) retornou o seguinte status:  
  
 HTTP_STATUS_DENIED 401  
  
 Verifique se os diretórios acessados pelo IIS têm as permissões adequadas. O RDS pode se comunicar com um servidor Web do IIS em execução em qualquer um dos três modos de autenticação de senha: desafio, básico ou anônimo/resposta do NT (chamado de autenticação integrada do Windows no Windows 2000). Além disso, o servidor Web deve ter permissões para o computador de fonte de dados se ele for um computador com Windows NT/Windows 2000.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos do RDS](./rds-fundamentals.md)