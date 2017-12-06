---
title: "Apêndice a-1 (DB2ToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c6a30367-d56f-4fcc-8920-c6a6b0335a67
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 795dca0b13d02613c3b59609dca52a61401bdf86
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="appendix---1-db2tosql"></a>Apêndice a-1 (DB2ToSQL)
Visão geral das opções de linha de comando do Console do SSMA:  
  
|SL. Nenhum.|Opção|Obrigatório?|Argumento de opção|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sim|scriptfile|Nome do arquivo XML válido.<br /><br />Arquivo de definição de Script do console.|  
|2|-v/variável|Não|variablevaluefile|Nome do arquivo XML válido.<br /><br />Se a variável for usada no arquivo de script, esse arquivo deve ser especificado.|  
|3|-c/serverconnection|Não|serverconnectionfile|Nome do arquivo XML válido.<br /><br />Esse arquivo contém informações de conexão do servidor.|  
|4|-x / xmloutput|Não|xmloutputfile|Esta opção indica a saída do console no formato XML. Se essa opção não for especificada, a saída padrão está no formato de texto.<br /><br />Se xmloutputfile não for especificado, a saída XML é direcionada para STDOUT.<br /><br />Xmloutputfile é o nome do arquivo para o qual a saída do console é gravada no formato XML.|  
|5|-l/log|Não|logfile|Nome de arquivo válido.|  
|6|-a e/projectenvironment|Não|projectenvironmentfolder|Nome de pasta válido que contém os arquivos do ambiente de projeto SSMA.|  
|7|-p/securepassword|Não|-a ou adicionar {< server_id > [,... n] &#124; tudo} – c &#124; serverconnection < arquivo de conexão servidor > [-v &#124; variável < arquivo de valor variável >] [-s/substituir]<br /><br />ou<br /><br />-a ou adicionar {< server_id > [,... n] &#124; tudo} – s &#124; script < arquivo de script > [-v &#124; variável < arquivo de valor variável >] [-s/substituir]<br /><br />– r/remover {< server_id > [,... n] &#124; tudo}<br /><br />lista / -l<br /><br />– e /Export {< server-id > [,... n] &#124; todos os} < senha criptografada - arquivo ><br /><br />– i / importação {< server-id > [,... n] &#124; tudo} < criptografado-senha-file >|Se especificado, essa opção não deve ser combinada com outras opções.<br /><br />id do servidor: fornecida uma ID exclusiva para um servidor {string}<br /><br />arquivo de conexão de servidor: arquivo de definição de servidor (serverconnectionfile ou scriptfile).<br /><br />arquivo de valores de variável: ele é um arquivo de definição da variável e usado no arquivo de conexão de servidor.<br /><br />senha – arquivo criptografado: é um arquivo de senhas do servidor criptografado usando uma frase secreta especificada pelo usuário.|  
|8|-?|Não|Não Aplicável|Não Aplicável|  
  
## <a name="see-also"></a>Consulte também  
[Executar o console do SSMA](http://msdn.microsoft.com/en-us/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  
