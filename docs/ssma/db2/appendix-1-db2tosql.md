---
title: Apêndice – 1 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c6a30367-d56f-4fcc-8920-c6a6b0335a67
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ee92addc2d77c8393c3378762618504344b8d477
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63453650"
---
# <a name="appendix---1-db2tosql"></a>Apêndice – 1 (DB2ToSQL)
Visão geral das opções de linha de comando do Console do SSMA:  
  
|SL. Não.|Alternar|Obrigatório?|Argumento de opção|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sim|scriptfile|Nome do arquivo XML válido.<br /><br />Arquivo de definição de Script de console.|  
|2|-v/variable|Não|variablevaluefile|Nome do arquivo XML válido.<br /><br />Se as variáveis são usadas no arquivo de script, esse arquivo deve ser especificado.|  
|3|-c/serverconnection|Não|serverconnectionfile|Nome do arquivo XML válido.<br /><br />Esse arquivo contém informações de conexão do servidor.|  
|4|-x/xmloutput|Não|xmloutputfile|Essa opção indica a saída do console no formato XML. Se essa opção não for especificada, a saída padrão está no formato de texto.<br /><br />Se xmloutputfile não for especificado, a saída XML é direcionada para STDOUT.<br /><br />Xmloutputfile é o nome do arquivo no qual a saída do console é gravada no formato XML.|  
|5|-l/log|Não|logfile|Nome de arquivo válido.|  
|6|-e/projectenvironment|Não|projectenvironmentfolder|Nome de pasta válido que contém os arquivos do ambiente de projeto SSMA.|  
|7|-p/securepassword|Não|-a/adicionar {< server_id > [,... n] &#124; todas as} - c&#124;serverconnection < server-conexão-file > [-v&#124;variável < arquivo de valor variável >] [-s/substituir]<br /><br />ou em<br /><br />-a/add {<server_id> [,...n] &#124; all} -s&#124;script <script-file> [-v&#124;variable <variable-value-file>] [-o/overwrite]<br /><br />-r/remove {<server_id> [, ...n] &#124; all}<br /><br />-l/list<br /><br />-e/export {<server-id> [, ...n] &#124; all} <encrypted-password -file><br /><br />-i/import {<server-id> [, ...n] &#124; all} <encrypted-password-file>|Se for especificado, essa opção não deve ser combinada com outras opções.<br /><br />server-id: Uma ID exclusiva fornecida para um servidor {string}<br /><br />arquivo de conexão de servidor: arquivo de definição de servidor (serverconnectionfile ou scriptfile).<br /><br />variable-value-file: Ele é um arquivo de definição de variável e usado no arquivo de conexão de servidor.<br /><br />criptografado--arquivo de senha: É um arquivo do servidor senhas criptografado usando uma frase secreta especificada pelo usuário.|  
|8|-?|Não|Não Aplicável|Não Aplicável|  
  
## <a name="see-also"></a>Consulte também  
[Executar o console do SSMA](https://msdn.microsoft.com/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  
