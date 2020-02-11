---
title: Apêndice-1 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 00665e16-2990-4bfc-8e17-d97ca9fb4999
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: ca084ec1849ab22940bb1617476637c105e90609
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68115027"
---
# <a name="appendix---1-accesstosql"></a>Apêndice-1 (AccessToSQL)
Exibição rápida das opções de linha de comando do console do SSMA:  
  
|SL. Não.|Opção|Necessário?|Argumento de opção|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sim|scriptfile|Nome de arquivo XML válido.<br /><br />Arquivo de definição de script do console.|  
|2|-v/variável|Não|variablevaluefile|Nome de arquivo XML válido. Se forem usadas variáveis no arquivo de script, esse arquivo deverá ser especificado.|  
|3|-c/ServerConnection|Não|serverconnectionfile|Nome de arquivo XML válido. Esse arquivo contém informações de conexão do servidor.|  
|4|-x/xmloutput|Não|xmlarquivo_de_saída|Essa opção indica a saída do console no formato XML. Se essa opção não for especificada, a saída padrão estará no formato de texto.<br /><br />Se xmloutputtypefile não for especificado, a saída XML será direcionada para STDOUT.<br /><br />Xmloutputtype é o nome do arquivo no qual a saída do console é gravada no formato XML.|  
|5|-l/log|Não|logfile|Nome de arquivo válido.|  
|6|-e/projectenvironment|Não|projectenvironmentfolder|Nome de pasta válido que contém arquivos de ambiente do projeto do SSMA.|  
|7|-p/SecurePassword|Não|-a/adicionar {<server_id> [,... n] &#124; All}-c&#124;ServerConnection <servidor-Connection-File> [-v&#124;Variable <variável-value-File>] [-o/overwrite]<br /><br />ou<br /><br />-a/adicionar {<server_id> [,... n] &#124; todos os}-s&#124;script <script-arquivo> [-v&#124;variável <variável-valor-arquivo>] [-o/substituir]<br /><br />-r/remover {<server_id> [,... n] &#124; todos}<br /><br />-l/lista<br /><br />-e/exportar {<Server-ID> [,... n] &#124; todos} <arquivo criptografado-senha><br /><br />-i/Import {<Server-ID> [,... n] &#124; todos} <arquivo criptografado-senha>|Se especificado, essa opção não deve ser combinada com nenhuma outra opção.<br /><br />Server-ID: uma ID exclusiva fornecida para um servidor {String}<br /><br />servidor-arquivo de conexão: arquivo de definição de servidor (serverconnectionfile ou scriptfile).<br /><br />variável-de-valor-arquivo: é um arquivo de definição de variável e usado no arquivo de conexão de servidor.<br /><br />Encrypt-password-file: é um arquivo de senhas de servidor criptografado usando uma frase secreta especificada pelo usuário.|  
|8|-?|Não|Não aplicável|Não aplicável|  
  
## <a name="see-also"></a>Consulte Também  
[Executando o console do SSMA (Access)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
