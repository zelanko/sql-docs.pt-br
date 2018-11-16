---
title: Apêndice – 1 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Appendix
ms.assetid: 6dcfd6d5-772c-4876-aa94-a7f43c4b9d59
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0b5b534e4b6d9152642dacd4b294476b6b9e71c6
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51663786"
---
# <a name="appendix---1-sybasetosql"></a>Apêndice – 1 (SybaseToSQL)
Visão geral das opções de linha de comando do Console do SSMA:  
  
|SL. Nenhum.|Opção|Obrigatório?|Argumento de opção|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sim|scriptfile|Nome do arquivo XML válido.<br /><br />Arquivo de definição de Script de console.|  
|2|-v/variável|não|variablevaluefile|Nome do arquivo XML válido.<br /><br />Se as variáveis são usadas no arquivo de script, esse arquivo deve ser especificado.|  
|3|-c/serverconnection|não|serverconnectionfile|Nome do arquivo XML válido.<br /><br />Esse arquivo contém informações de conexão do servidor.|  
|4|-x/xmloutput|não|xmloutputfile|Essa opção indica a saída do console no formato XML. Se essa opção não for especificada, a saída padrão está no formato de texto.<br /><br />Se xmloutputfile não for especificado, a saída XML é direcionada para STDOUT.<br /><br />Xmloutputfile é o nome do arquivo no qual a saída do console é gravada no formato XML.|  
|5|-l/log|não|logfile|Nome de arquivo válido.|  
|6|-e/projectenvironment|não|projectenvironmentfolder|Nome de pasta válido que contém os arquivos do ambiente de projeto SSMA.|  
|7|-p/securepassword|não|-a/adicionar {< server_id > [,... n] &#124; todas as} – c&#124;serverconnection < server-conexão-file > [-v&#124;variável < arquivo de valor variável >] [-s/substituir]<br /><br />ou em<br /><br />-a/adicionar {< server_id > [,... n] &#124; todas as} – s&#124;script < arquivo de script > [-v&#124;variável < arquivo de valor variável >] [-s/substituir]<br /><br />– r/remover {< server_id > [,... n] &#124; todos os}<br /><br />-l/lista<br /><br />– e/exportação {< server-id > [,... n] &#124; todas as} < criptografado-password - arquivo ><br /><br />– i / Importar {< server-id > [,... n] &#124; todas as} < criptografado-senha-file >|Se for especificado, essa opção não deve ser combinada com outras opções.<br /><br />id do servidor: uma ID exclusiva fornecida para um servidor {string}<br /><br />arquivo de conexão de servidor: arquivo de definição de servidor (serverconnectionfile ou scriptfile).<br /><br />arquivo de valores de variável: ele é um arquivo de definição de variável e usado no arquivo de conexão de servidor.<br /><br />criptografado-– arquivo de senha: é um arquivo do servidor senhas criptografado usando uma frase secreta especificada pelo usuário.|  
|8|-?|não|Não Aplicável|Não Aplicável|  
  
## <a name="see-also"></a>Consulte também  
[Executar o Console do SSMA (Sybasetosql)](https://msdn.microsoft.com/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
