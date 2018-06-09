---
title: Apêndice a-1 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 00665e16-2990-4bfc-8e17-d97ca9fb4999
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c97b1f8c85b9d90d9e580f2b2cc4c517855e3abf
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773102"
---
# <a name="appendix---1-accesstosql"></a>Apêndice a-1 (AccessToSQL)
Visão geral das opções de linha de comando do Console do SSMA:  
  
|SL. Nenhum.|Opção|Obrigatório?|Argumento de opção|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sim|scriptfile|Nome do arquivo XML válido.<br /><br />Arquivo de definição de Script do console.|  
|2|-v/variável|não|variablevaluefile|Nome do arquivo XML válido. Se a variável for usada no arquivo de script, esse arquivo deve ser especificado.|  
|3|-c/serverconnection|não|serverconnectionfile|Nome do arquivo XML válido. Esse arquivo contém informações de conexão do servidor.|  
|4|-x/xmloutput|não|xmloutputfile|Esta opção indica a saída do console no formato XML. Se essa opção não for especificada, a saída padrão está no formato de texto.<br /><br />Se xmloutputfile não for especificado, a saída XML é direcionada para STDOUT.<br /><br />Xmloutputfile é o nome do arquivo para o qual a saída do console é gravada no formato XML.|  
|5|-l/log|não|logfile|Nome de arquivo válido.|  
|6|-e/projectenvironment|não|projectenvironmentfolder|Nome de pasta válido que contém os arquivos do ambiente de projeto SSMA.|  
|7|-p/securepassword|não|-a ou adicionar {< server_id > [,... n] &#124; todos os} – c&#124;serverconnection < arquivo de conexão servidor > [-v&#124;variável < arquivo de valor variável >] [-s/substituir]<br /><br />ou em<br /><br />-a ou adicionar {< server_id > [,... n] &#124; todos os} – s&#124;script < arquivo de script > [-v&#124;variável < arquivo de valor variável >] [-s/substituir]<br /><br />– r/remover {< server_id > [,... n] &#124; todos os}<br /><br />lista / -l<br /><br />– e /Export {< server-id > [,... n] &#124; todos os} < senha criptografada - arquivo ><br /><br />– i / importação {< server-id > [,... n] &#124; todos os} < criptografado-senha-file >|Se especificado, essa opção não deve ser combinada com outras opções.<br /><br />id do servidor: fornecida uma ID exclusiva para um servidor {string}<br /><br />arquivo de conexão de servidor: arquivo de definição de servidor (serverconnectionfile ou scriptfile).<br /><br />arquivo de valores de variável: ele é um arquivo de definição da variável e usado no arquivo de conexão de servidor.<br /><br />senha – arquivo criptografado: é um arquivo de senhas do servidor criptografado usando uma frase secreta especificada pelo usuário.|  
|8|-?|não|Não Aplicável|Não Aplicável|  
  
## <a name="see-also"></a>Consulte também  
[Executar o Console do SSMA (acesso)](http://msdn.microsoft.com/en-us/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
