---
title: Apêndice – 1 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e01f8be5-ce68-4c9f-bd13-d65e73a16470
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 2539ac90fcce2dd1d5b30384c07bac620d809f0a
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51668235"
---
# <a name="appendix---1-oracletosql"></a>Apêndice – 1 (OracleToSQL)
Visão geral das opções de linha de comando do Console do SSMA:  
  
|SL. Nenhum.|Opção|Obrigatório?|Argumento de opção|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sim|scriptfile|Nome do arquivo XML válido.<br /><br />Arquivo de definição de Script de console.|  
|2|-v/variável|não|variablevaluefile|Nome do arquivo XML válido.<br /><br />Se as variáveis são usadas no arquivo de script, esse arquivo deve ser especificado.|  
|3|-c/serverconnection|não|serverconnectionfile|Nome do arquivo XML válido.<br /><br />Esse arquivo contém informações de conexão do servidor.|  
|4|-x/xmloutput|não|xmloutputfile|Essa opção indica a saída do console no formato XML. Se essa opção não for especificada, a saída padrão está no formato de texto.<br /><br />Se xmloutputfile não for especificado, a saída XML é direcionada para `STDOUT`.<br /><br />Xmloutputfile é o nome do arquivo no qual a saída do console é gravada no formato XML.|  
|5|-l/log|não|logfile|Nome de arquivo válido.|  
|6|-e/projectenvironment|não|projectenvironmentfolder|Nome de pasta válido que contém os arquivos do ambiente de projeto SSMA.|  
|7|-p/securepassword|não|-a/adicionar {< server_id > [,... n] &#124; todas as} – c&#124;serverconnection < server-conexão-file > [-v&#124;variável < arquivo de valor variável >] [-s/substituir]<br /><br />ou em<br /><br />-a/adicionar {< server_id > [,... n] &#124; todas as} – s&#124;script < arquivo de script > [-v&#124;variável < arquivo de valor variável >] [-s/substituir]<br /><br />– r/remover {< server_id > [,... n] &#124; todos os}<br /><br />-l/lista<br /><br />– e/exportação {< server-id > [,... n] &#124; todas as} < criptografado-password - arquivo ><br /><br />– i / Importar {< server-id > [,... n] &#124; todas as} < criptografado-senha-file >|Se for especificado, essa opção não deve ser combinada com outras opções.<br /><br />id do servidor: uma ID exclusiva fornecida para um servidor {string}<br /><br />arquivo de conexão de servidor: arquivo de definição de servidor (serverconnectionfile ou scriptfile).<br /><br />arquivo de valores de variável: ele é um arquivo de definição de variável e usado no arquivo de conexão de servidor.<br /><br />arquivo criptografado de senha: é um arquivo do servidor senhas criptografado usando uma frase secreta especificada pelo usuário.|  
|8|-?|não|Não Aplicável|Não Aplicável|  
  
## <a name="see-also"></a>Consulte também  
[Executar o Console do SSMA (Oracle)](https://msdn.microsoft.com/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
