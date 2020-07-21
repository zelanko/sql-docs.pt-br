---
title: MSSQLSERVER_833 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 833 (Database Engine error)
ms.assetid: 14129cc4-be80-4772-9e3f-0e5da4d0696b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ceccd88d57a934da69bead726399edf2b39d45be
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553181"
---
# <a name="mssqlserver_833"></a>MSSQLSERVER_833
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|833|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|BUF_LONG_IO|  
|Texto da mensagem|SQL Server encontrou% d ocorrência (s) de solicitações de e/s demorando mais do que% d segundos para serem concluídas no arquivo [% ls] no banco de dados `[%ls] (%d)` .  O identificador de arquivo do SO é 0x%p.  O deslocamento da E/S mais demorada é: %#016I64x.|  
  
## <a name="explanation"></a>Explicação  
 Esta mensagem indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emitiu uma solicitação de leitura ou gravação de disco, e que a solicitação demorou mais de 15 segundos para retornar. Esse erro é informado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e indica um problema com o subsistema de E/S.  
  
### <a name="possible-causes"></a>Possíveis causas  
 Esse problema pode ser causado por problemas de desempenho do sistema, erros de hardware, erros de firmware, problemas de driver de dispositivo ou intervenção de driver de filtro no processo de E/S.  
  
## <a name="user-action"></a>Ação do usuário  
 Solucione este erro procurando mensagens de erros relacionados a hardware no log de eventos de sistema. Examine também os logs específicos do hardware, se estiverem disponíveis.  
  
 Use o Monitor de Desempenho para examinar os seguintes contadores:  
  
-   **Média de seg/transferência do disco**  
  
-   **Média de comprimento da fila do disco**  
  
-   **Comprimento atual da fila do disco**  
  
 Por exemplo, o tempo da **Média de seg/transferência do disco** em um computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], normalmente, é inferior a 15 milissegundos. Se o valor da **Média de seg/transferência do disco** aumentar, isso indicará que o subsistema de E/S não está acompanhando a demanda de E/S.  
  
> [!NOTE]  
>  O acesso ao disco pode ficar mais lento devido a um programa antivírus. Para aumentar a velocidade de acesso, exclua os arquivos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificados na mensagem de erro das verificações ativas de vírus.  
  
 Para obter mais informações sobre erros de E/S, consulte [Noções básicas de E/S do Microsoft SQL Server, Capítulo 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10)) e o artigo da Base de Dados de Conhecimento em [https://support.microsoft.com/kb/897284](https://support.microsoft.com/kb/897284).  
  
  
