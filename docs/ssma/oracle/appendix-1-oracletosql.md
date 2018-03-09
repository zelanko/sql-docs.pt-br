---
title: "Apêndice a-1 (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e01f8be5-ce68-4c9f-bd13-d65e73a16470
caps.latest.revision: "15"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 8e415cb8fddf1a2c37fa44f38ff23a2c5c64c568
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="appendix---1-oracletosql"></a>Apêndice a-1 (OracleToSQL)
Visão geral das opções de linha de comando do Console do SSMA:  
  
|SL. Nenhum.|Opção|Obrigatório?|Argumento de opção|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sim|scriptfile|Nome do arquivo XML válido.<br /><br />Arquivo de definição de Script do console.|  
|2|-v/variável|não|variablevaluefile|Nome do arquivo XML válido.<br /><br />Se a variável for usada no arquivo de script, esse arquivo deve ser especificado.|  
|3|-c/serverconnection|não|serverconnectionfile|Nome do arquivo XML válido.<br /><br />Esse arquivo contém informações de conexão do servidor.|  
|4|-x / xmloutput|não|xmloutputfile|Esta opção indica a saída do console no formato XML. Se essa opção não for especificada, a saída padrão está no formato de texto.<br /><br />Se xmloutputfile não for especificado, a saída XML é direcionada para `STDOUT`.<br /><br />Xmloutputfile é o nome do arquivo para o qual a saída do console é gravada no formato XML.|  
|5|-l/log|não|logfile|Nome de arquivo válido.|  
|6|-a e/projectenvironment|não|projectenvironmentfolder|Nome de pasta válido que contém os arquivos do ambiente de projeto SSMA.|  
|7|-p/securepassword|não|-a ou adicionar {< server_id > [,... n] &#124; tudo} – c &#124; serverconnection < arquivo de conexão servidor > [-v &#124; variável < arquivo de valor variável >] [-s/substituir]<br /><br />ou em<br /><br />-a ou adicionar {< server_id > [,... n] &#124; tudo} – s &#124; script < arquivo de script > [-v &#124; variável < arquivo de valor variável >] [-s/substituir]<br /><br />– r/remover {< server_id > [,... n] &#124; tudo}<br /><br />lista / -l<br /><br />– e /Export {< server-id > [,... n] &#124; todos os} < senha criptografada - arquivo ><br /><br />– i / importação {< server-id > [,... n] &#124; tudo} < criptografado-senha-file >|Se especificado, essa opção não deve ser combinada com outras opções.<br /><br />id do servidor: fornecida uma ID exclusiva para um servidor {string}<br /><br />arquivo de conexão de servidor: arquivo de definição de servidor (serverconnectionfile ou scriptfile).<br /><br />arquivo de valores de variável: ele é um arquivo de definição da variável e usado no arquivo de conexão de servidor.<br /><br />arquivo criptografado de senha: é um arquivo de senhas do servidor criptografado usando uma frase secreta especificada pelo usuário.|  
|8|-?|não|Não Aplicável|Não Aplicável|  
  
## <a name="see-also"></a>Consulte Também  
[Executar o Console do SSMA (Oracle)](http://msdn.microsoft.com/en-us/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
