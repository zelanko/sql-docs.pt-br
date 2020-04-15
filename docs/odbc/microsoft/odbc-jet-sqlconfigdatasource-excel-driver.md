---
title: ODBC Jet SQLConfigDataSource (Driver Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a76482acd1182d900336d7ac9826b16968e00caa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293006"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas do Excel Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 A função **SQLConfigDataSource,** usada para adicionar, modificar ou excluir uma fonte de dados, usa dinamicamente as seguintes palavras-chave.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|Dbq|Para o driver microsoft excel ao acessar arquivos Microsoft Excel 5.0 ou posteriores, o nome do arquivo da pasta de trabalho.<br /><br /> Isso define a mesma opção que o **Banco de Dados** na caixa de diálogo de configuração.|  
|Defaultdir|A especificação do caminho para o diretório.<br /><br /> Isso define a mesma opção que **Selecionar diretório** ou selecionar a área **de trabalho** na caixa de diálogo de configuração.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção **que Description** na caixa de diálogo de configuração.|  
|DRIVER|A especificação do caminho para o driver DLL.|  
|DRIVERID|Uma id inteira para o motorista.<br /><br /> 534 (Microsoft Excel 3.0)<br /><br /> 278 (Microsoft Excel 4.0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|Fil|Tipo de arquivo, por exemplo, Excel 3.0, Excel 4.0, Excel 5.0, Excel 7.0, Excel 97, Excel 2000 ou Excel 2003.|  
|NOMES DE FIRSTROWHAS|Indica se as células da primeira linha da faixa contêm os nomes da coluna para a tabela (1) ou não (0).|  
|MAXSCANROWS|O número de linhas a serem digitalizadas ao definir o tipo de dados de uma coluna com base nos dados existentes.<br /><br /> Um número de 1 a 16 pode ser inserido para as linhas para escanear. O valor é padrão para 8; se for definido como 0, todas as linhas são digitalizadas. (Um número fora do limite retornará um erro.)<br /><br /> Isso define a mesma opção **que Linhas para Scan na** caixa de diálogo de configuração.|  
|READONLY|TRUE para tornar somente leitura de arquivo; FALSO para fazer o arquivo não ler somente.<br /><br /> Isso define a mesma opção **que Read Only** na caixa de diálogo de configuração.|  
|Tópicos|O número de roscas de fundo para o motor usar. Para o driver Microsoft Access, esse valor é padrão para 3, mas pode ser alterado. Para o dBASE, MicrosoftExceldriver este valor é 3 e não pode ser alterado.<br /><br /> Isso define a mesma opção **que os Threads** na caixa de diálogo de configuração.|
