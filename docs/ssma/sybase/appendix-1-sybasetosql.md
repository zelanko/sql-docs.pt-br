---
title: Apêndice a-1 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Appendix
ms.assetid: 6dcfd6d5-772c-4876-aa94-a7f43c4b9d59
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c33a941991c8be58e6437426c95ee807f5e8554
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="appendix---1-sybasetosql"></a>Apêndice a-1 (SybaseToSQL)
Visão geral das opções de linha de comando do Console do SSMA:  
  
|Sl. Nenhum.|Opção|Obrigatório?|Argumento de opção|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sim|scriptfile|Nome do arquivo XML válido.<br /><br />Arquivo de definição de Script do console.|  
|2|-v/variável|não|variablevaluefile|Nome do arquivo XML válido.<br /><br />Se a variável for usada no arquivo de script, esse arquivo deve ser especificado.|  
|3|-c/serverconnection|não|serverconnectionfile|Nome do arquivo XML válido.<br /><br />Esse arquivo contém informações de conexão do servidor.|  
|4|-x/xmloutput|não|xmloutputfile|Esta opção indica a saída do console no formato XML. Se essa opção não for especificada, a saída padrão está no formato de texto.<br /><br />Se xmloutputfile não for especificado, a saída XML é direcionada para STDOUT.<br /><br />Xmloutputfile é o nome do arquivo para o qual a saída do console é gravada no formato XML.|  
|5|-l/log|não|logfile|Nome de arquivo válido.|  
|6|-e/projectenvironment|não|projectenvironmentfolder|Nome de pasta válido que contém os arquivos do ambiente de projeto SSMA.|  
|7|-p/securepassword|não|-a ou adicionar {< server_id > [,... n] &#124; todos os} – c&#124;serverconnection < arquivo de conexão servidor > [-v&#124;variável < arquivo de valor variável >] [-s/substituir]<br /><br />ou<br /><br />-a ou adicionar {< server_id > [,... n] &#124; todos os} – s&#124;script < arquivo de script > [-v&#124;variável < arquivo de valor variável >] [-s/substituir]<br /><br />–r/remove {<server_id> [, …n] &#124; all}<br /><br />lista / -l<br /><br />– e /Export {< server-id > [,... n] &#124; todos os} < senha criptografada - arquivo ><br /><br />– i / importação {< server-id > [,... n] &#124; todos os} < criptografado-senha-file >|Se especificado, essa opção não deve ser combinada com outras opções.<br /><br />id do servidor: fornecida uma ID exclusiva para um servidor {string}<br /><br />arquivo de conexão de servidor: arquivo de definição de servidor (serverconnectionfile ou scriptfile).<br /><br />arquivo de valores de variável: ele é um arquivo de definição da variável e usado no arquivo de conexão de servidor.<br /><br />senha – arquivo criptografado: é um arquivo de senhas do servidor criptografado usando uma frase secreta especificada pelo usuário.|  
|8|-?|não|Não Aplicável|Não Aplicável|  
  
## <a name="see-also"></a>Consulte também  
[Executar o Console do SSMA (Sybase)](http://msdn.microsoft.com/en-us/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
