---
title: Apêndice – 1 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 00665e16-2990-4bfc-8e17-d97ca9fb4999
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 521c94fe15c8409377997edfc0b5821f92bed34d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52533326"
---
# <a name="appendix---1-accesstosql"></a>Apêndice – 1 (AccessToSQL)
Visão geral das opções de linha de comando do Console do SSMA:  
  
|SL. Nenhum.|Alternar|Obrigatório?|Argumento de opção|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sim|scriptfile|Nome do arquivo XML válido.<br /><br />Arquivo de definição de Script de console.|  
|2|-v/variável|Não|variablevaluefile|Nome do arquivo XML válido. Se as variáveis são usadas no arquivo de script, esse arquivo deve ser especificado.|  
|3|-c/serverconnection|Não|serverconnectionfile|Nome do arquivo XML válido. Esse arquivo contém informações de conexão do servidor.|  
|4|-x/xmloutput|Não|xmloutputfile|Essa opção indica a saída do console no formato XML. Se essa opção não for especificada, a saída padrão está no formato de texto.<br /><br />Se xmloutputfile não for especificado, a saída XML é direcionada para STDOUT.<br /><br />Xmloutputfile é o nome do arquivo no qual a saída do console é gravada no formato XML.|  
|5|-l/log|Não|logfile|Nome de arquivo válido.|  
|6|-e/projectenvironment|Não|projectenvironmentfolder|Nome de pasta válido que contém os arquivos do ambiente de projeto SSMA.|  
|7|-p/securepassword|Não|-a/adicionar {< server_id > [,... n] &#124; todas as} - c&#124;serverconnection < server-conexão-file > [-v&#124;variável < arquivo de valor variável >] [-s/substituir]<br /><br />ou em<br /><br />-a/adicionar {< server_id > [,... n] &#124; todas as} -s&#124;script < arquivo de script > [-v&#124;variável < arquivo de valor variável >] [-s/substituir]<br /><br />-r/remover {< server_id > [,... n] &#124; todos os}<br /><br />-l/lista<br /><br />-a e/exportação {< server-id > [,... n] &#124; todas as} < criptografado-password - arquivo ><br /><br />-i / Importar {< server-id > [,... n] &#124; todas as} < criptografado-senha-file >|Se for especificado, essa opção não deve ser combinada com outras opções.<br /><br />id do servidor: Uma ID exclusiva fornecida para um servidor {string}<br /><br />arquivo de conexão de servidor: arquivo de definição de servidor (serverconnectionfile ou scriptfile).<br /><br />valor de arquivo variável: Ele é um arquivo de definição de variável e usado no arquivo de conexão de servidor.<br /><br />criptografado--arquivo de senha: É um arquivo do servidor senhas criptografado usando uma frase secreta especificada pelo usuário.|  
|8|-?|Não|Não Aplicável|Não Aplicável|  
  
## <a name="see-also"></a>Consulte também  
[Executar o Console do SSMA (acesso)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
