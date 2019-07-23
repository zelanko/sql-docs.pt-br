---
title: Codificação por cores em editores de consultas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Query Editor [SQL Server Management Studio], color coding
- color coding [Query Editor]
ms.assetid: 802882dc-c997-4e3f-8a01-994bb43169ae
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a562e65b84abc7c952abe992ee2a63c9b0fa22d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68256679"
---
# <a name="color-coding-in-query-editors"></a>Codificação por cores no Editor de Consultas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  É atribuída uma categoria ao texto inserido nos editores de códigos; cada categoria é identificada por uma cor. As cores ajudam você a localizar rapidamente o texto no código. Por exemplo, os comentários se destacam em verde-escuro. A tabela a seguir lista as cores mais comuns. Você pode exibir a lista completa de cores e suas categorias, e configurar um esquema de cores personalizado usando o menu **Ferramentas**, **Opções** . Para obter mais informações sobre como alterar as cores padrão, veja [Alterar cor, tamanho e estilo da fonte](../../relational-databases/scripting/change-font-color-size-and-style.md).  
  
## <a name="default-code-colors"></a>Cores de código padrão  
  
|Color|Categoria|  
|-----------|--------------|  
|Vermelho|Cadeia de caracteres SQL|  
|Verde-escuro|Comentário|  
|Preto sobre fundo prateado|Comando SQLCMD|  
|Magenta|Função do sistema|  
|Verde|Tabela, exibição ou função com valor de tabela do sistema. Além disso, esquemas do sistema, sys e INFORMATION_SCHEMA.|  
|Azul|Palavra-chave|  
|Azul-petróleo|Números de linha ou parâmetro de modelo|  
|Castanho|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimento armazenado|  
|Cinza escuro|Operadores|  
  
## <a name="status-bar"></a>Barra de Status  
 Você pode configurar servidores registrados ou servidores [!INCLUDE[ssDE](../../includes/ssde-md.md)] em Pesquisador de Objetos para ter cores diferentes na barra de status do Editor de Consulta [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Isso o ajuda a identificar a qual servidor cada janela de editor é conectada quando você tem muitas janelas abertas ao mesmo tempo. Para obter mais informações sobre como definir cores da barra de status, veja [Barra de status &#40;Editor de Consultas do Mecanismo de Banco de Dados&#41;](../../relational-databases/scripting/status-bar-database-engine-query-editor.md).  
  
 Alguns tipos de editores não exibem a barra de status ou não oferecem suporte a várias cores.  
  
  
