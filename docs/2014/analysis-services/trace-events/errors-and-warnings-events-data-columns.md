---
title: Erros e avisos de colunas de dados de eventos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Errors and Warnings event category [SQL Server]
ms.assetid: f375d303-7aab-4c51-a955-05a2762cc4d1
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8d1af0dc17026c5003444a9d626708a0a86056b5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119205"
---
# <a name="errors-and-warnings-events-data-columns"></a>Colunas de dados de eventos de erros e de avisos
  A categoria de evento de segurança de auditoria tem a seguinte classe de evento:  
  
-   Classe de erro  
  
 A tabela a seguir lista as colunas de dados dessa classe de evento.  
  
## <a name="error-event-classdata-columns"></a>Classe Error Event - Colunas de dados  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|StartTime|3|5|Contém a hora em que o evento iniciou, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|SessionType|8|8|Contém o tipo de entidade que causou o erro.|  
|Severity|22|1|Contém o nível de severidade de uma exceção associada ao evento de erro. Os valores são:<br /><br /> 0 = Êxito<br /><br /> 1 = Informativo<br /><br /> 2 = Aviso<br /><br /> 3 = Erro|  
|Success|23|1|Contém o êxito ou a falha do evento de erro. Os valores são:<br /><br /> 0 = Falha<br /><br /> 1 = Êxito|  
|Erro|24|1|Contém o número de qualquer erro associado ao evento de erro.|  
|ConnectionID|25|1|Contém a ID de conexão exclusiva associada ao evento de erro.|  
|DatabaseName|28|8|Contém o nome da instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual o evento de erro ocorreu.|  
|NTUserName|32|8|Contém o nome de usuário do Windows associado ao evento de erro.|  
|NTDomainName|33|8|Contém a conta de domínio do Windows associada ao evento de logon.|  
|ClientHostName|35|8|Contém o nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente.|  
|ClientProcessID|36|1|Contém a ID de processo do aplicativo cliente.|  
|ApplicationName|37|8|Contém o nome do aplicativo cliente que criou a conexão com o servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|SessionID|39|8|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento de erro. A SPID corresponde diretamente à GUID de sessão usada pelo XML for Analysis (XMLA).|  
|SPID|41|1|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento de erro. A SPID corresponde diretamente à GUID de sessão usada pelo XML for Analysis (XMLA).|  
|TextData|42|9|Contém os dados de texto associados ao evento de erro.|  
|ServerName|43|8|Contém o nome do servidor que executa a instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual o evento de erro ocorreu.|  
  
## <a name="see-also"></a>Consulte também  
 [Categoria de evento de auditoria de segurança](security-audit-event-category.md)  
  
  