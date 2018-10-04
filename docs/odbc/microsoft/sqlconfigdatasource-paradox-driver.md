---
title: SQLConfigDataSource (Driver do Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad9c944af33da86e0d4f85769288f4ab7b6c369f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694584"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (Driver do Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Paradox. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O **SQLConfigDataSource** função que é usada para adicionar, modificar ou excluir uma fonte de dados usa as seguintes palavras-chave dinamicamente.  
  
|Palavra-chave|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|A sequência na qual os campos são classificados.<br /><br /> Quando o driver do Paradox é usado, a sequência pode ser ASCII (padrão), internacionais, finlandês-sueco ou dinamarquês-norueguês.<br /><br /> Isso define a mesma opção como **sequência de agrupamento** na caixa de diálogo de instalação.|  
|DBQ|O nome do arquivo de banco de dados.<br /><br /> Isso define a mesma opção como **banco de dados** na caixa de diálogo de instalação.|  
|DEFAULTDIR|A especificação de caminho para o diretório.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção como **descrição** na caixa de diálogo de instalação.|  
|DRIVER|A especificação de caminho para a DLL do driver.|  
|DRIVERID|Uma ID de inteiro para o driver.<br /><br /> 26 (paradox 3. x)<br /><br /> 282 (paradox 4. x)<br /><br /> 538 (paradox 5. x)|  
|EXCLUSIVO|Determina se o banco de dados será aberto no modo exclusivo (acessado somente por um usuário por vez) ou (acessado por mais de um usuário por vez) de modo compartilhado. Pode ser verdadeiro (modo exclusivo) ou falso (modo compartilhado).<br /><br /> Isso define a mesma opção como **exclusivo** na caixa de diálogo de instalação.|  
|FIL|Tipo Paradox arquivo 3. x, Paradox 4. x ou Paradox 5. x|  
|TIPO DE ARQUIVO|Tipo de arquivo para o driver de texto (texto).|  
|PAGETIMEOUT|Especifica o período de tempo, em décimos de segundo, que uma página (se não usado) permanece no buffer antes de serem removidos. O padrão é 600 décimos de segundo (60 segundos). Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção como **Page Timeout** na caixa de diálogo de instalação.|  
|PARADOXNETPATH|O caminho completo do diretório que contém um banco de dados de bloqueio do Paradox, porque ela contém o arquivo PDOXUSRS.net (no Paradox 4. *x*) ou o arquivo PARADOX.net (no Paradox 5. *x*). Se o diretório não contiver um desses arquivos, o driver do Paradox criará um. Para obter informações sobre esses arquivos, consulte a documentação do Paradox.<br /><br /> Antes de um diretório de rede pode ser selecionado, um nome de usuário do Paradox deve ser inserido.<br /><br /> Isso define a mesma opção como **selecione o diretório de rede** na caixa de diálogo de instalação.|  
|PARADOXNETSTYLE|Para o driver do Paradox, a rede acesso estilo a ser usado ao acessar dados Paradox: qualquer um dos "3. x" para Paradox 3. *x* ou "4. x" para Paradox 4. *x* ou 5. *x*. Pode ser definido como "3. x" ou "4. x" se a versão for Paradox 4. *x* ou 5. *x*; se a versão for Paradox 3. *x*, o estilo deve ser "3. x".<br /><br /> Isso define a mesma opção como **estilo Net** na caixa de diálogo de instalação.|  
|PARADOXUSERNAME|Para o driver do Paradox, o nome de usuário do Paradox.<br /><br /> Isso define a mesma opção como **nome de usuário** na caixa de diálogo de instalação.|  
|PWD|A senha.<br /><br /> Essa é uma palavra-chave opcional e nunca será gravada no arquivo do driver. Ele é usado em uma chamada para **SQLDriverConnect** em relação aos arquivos do Paradox protegido por senha. A senha usada serão válida sempre que uma tabela é aberta. Se nenhuma senha for passada na cadeia de conexão, nenhuma senha é estabelecida para a tabela. Se tabelas tem senhas diferentes, mais de um não pode ser aberto na mesma sessão, nem as tabelas podem ser unidas.|  
|READONLY|TRUE para tornar o arquivo somente leitura; FALSE para tornar o arquivo não é somente leitura.<br /><br /> Isso define a mesma opção como **somente leitura** na caixa de diálogo de instalação.|  
|THREADS|O número de threads em segundo plano para o mecanismo a ser usado. Esse valor é 3 e não pode ser alterado.<br /><br /> Isso define a mesma opção como **Threads** na caixa de diálogo de instalação.|
