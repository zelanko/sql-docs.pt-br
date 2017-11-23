---
title: SQLConfigDataSource (Driver Paradox) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 18d184fa68e1b8a9d87f6c4e86e5059c7f7a118d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (Paradox Driver)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver Paradox. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O **SQLConfigDataSource** função que é usada para adicionar, modificar ou excluir uma fonte de dados dinamicamente usa as seguintes palavras-chave.  
  
|Palavra-chave|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|A sequência na qual os campos são classificados.<br /><br /> Quando o driver do Paradox é usado, a sequência pode ser ASCII (padrão), internacional, finlandês-sueco ou dinamarquês-norueguês.<br /><br /> Isso define a mesma opção como **sequência de agrupamento** na caixa de diálogo de instalação.|  
|DBQ|O nome do arquivo de banco de dados.<br /><br /> Isso define a mesma opção como **banco de dados** na caixa de diálogo de instalação.|  
|DEFAULTDIR|A especificação de caminho para o diretório.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção como **descrição** na caixa de diálogo de instalação.|  
|DRIVER|A especificação de caminho para a DLL do driver.|  
|DRIVERID|Uma ID de inteiro para o driver.<br /><br /> 26 (paradox 3. x)<br /><br /> 282 (paradox 4. x)<br /><br /> 538 (paradox 5. x)|  
|EXCLUSIVO|Determina se o banco de dados será aberto no modo exclusivo (acessado somente por um usuário por vez) ou (acessado por mais de um usuário por vez) de modo compartilhado. Pode ser verdadeiro (modo exclusivo) ou falso (modo compartilhado).<br /><br /> Isso define a mesma opção como **exclusivo** na caixa de diálogo de instalação.|  
|FIL|Arquivo tipo Paradox 3. x, Paradox 4. x ou Paradox 5. x|  
|TIPO DE ARQUIVO|Tipo de arquivo para o driver de texto (texto).|  
|PAGETIMEOUT|Especifica o período de tempo, em décimos de segundo, que uma página (se não usado) permanece no buffer antes de serem removidos. O padrão é 600 décimos de segundo (60 segundos). Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção como **Page Timeout** na caixa de diálogo de instalação.|  
|PARADOXNETPATH|O caminho completo do diretório que contém um banco de dados de bloqueio do Paradox, porque ele contém o arquivo PDOXUSRS.net (no Paradox 4. *x*) ou o arquivo PARADOX.net (no Paradox 5. *x*). Se o diretório não contiver um desses arquivos, o driver do Paradox criará um. Para obter informações sobre esses arquivos, consulte a documentação do Paradox.<br /><br /> Antes de um diretório de rede pode ser selecionado, um nome de usuário do Paradox deve ser inserido.<br /><br /> Isso define a mesma opção como **Selecionar pasta de rede** na caixa de diálogo de instalação.|  
|PARADOXNETSTYLE|Para o driver do Paradox, a rede acesso estilo a ser usado ao acessar dados Paradox: o "3. x" para o Paradox 3. *x* ou "4. x" para o Paradox 4. *x* ou 5. *x*. Pode ser definido como "3. x" ou "4. x", se a versão for Paradox 4. *x* ou 5. *x*; se a versão for Paradox 3. *x*, o estilo deve ser "3. x".<br /><br /> Isso define a mesma opção como **estilo Net** na caixa de diálogo de instalação.|  
|PARADOXUSERNAME|Para o driver do Paradox, o nome de usuário do Paradox.<br /><br /> Isso define a mesma opção como **nome de usuário** na caixa de diálogo de instalação.|  
|PWD|A senha.<br /><br /> Isso é uma palavra-chave opcional e nunca será gravado no arquivo pelo driver. Ele é usado em uma chamada para **SQLDriverConnect** em arquivos do Paradox protegido por senha. A senha usada serão válida sempre que uma tabela é aberta. Se nenhuma senha for transmitida na cadeia de conexão, nenhuma senha é estabelecida para essa tabela. Se tabelas tem senhas diferentes, mais de um não pode ser aberto na mesma sessão, nem as tabelas podem ser unidas.|  
|READONLY|TRUE para tornar o arquivo somente leitura; FALSE para tornar o arquivo não é somente leitura.<br /><br /> Isso define a mesma opção como **somente leitura** na caixa de diálogo de instalação.|  
|THREADS|O número de threads de plano de fundo para o mecanismo de usar. Esse valor é 3 e não pode ser alterado.<br /><br /> Isso define a mesma opção como **Threads** na caixa de diálogo de instalação.|
