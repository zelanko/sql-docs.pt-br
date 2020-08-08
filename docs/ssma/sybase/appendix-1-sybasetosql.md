---
title: Apêndice-1 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Appendix
ms.assetid: 6dcfd6d5-772c-4876-aa94-a7f43c4b9d59
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: ccd075529e5ecb3277ab698632cca9c948802690
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87932287"
---
# <a name="appendix---1-sybasetosql"></a>Apêndice – 1 (SybaseToSQL)
Exibição rápida das opções de linha de comando do console do SSMA:  
  
|SL. Não.|Alternar|Necessário?|Argumento de opção|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sim|scriptfile|Nome de arquivo XML válido.<br /><br />Arquivo de definição de script do console.|  
|2|-v/variável|Não|variablevaluefile|Nome de arquivo XML válido.<br /><br />Se forem usadas variáveis no arquivo de script, esse arquivo deverá ser especificado.|  
|3|-c/ServerConnection|Não|serverconnectionfile|Nome de arquivo XML válido.<br /><br />Esse arquivo contém informações de conexão do servidor.|  
|4|-x/xmloutput|Não|xmlarquivo_de_saída|Essa opção indica a saída do console no formato XML. Se essa opção não for especificada, a saída padrão estará no formato de texto.<br /><br />Se xmloutputtypefile não for especificado, a saída XML será direcionada para STDOUT.<br /><br />Xmloutputtype é o nome do arquivo no qual a saída do console é gravada no formato XML.|  
|5|-l/log|Não|logfile|Nome de arquivo válido.|  
|6|-e/projectenvironment|Não|projectenvironmentfolder|Nome de pasta válido que contém arquivos de ambiente do projeto do SSMA.|  
|7|-p/SecurePassword|Não|-a/adicionar {<server_id> [,... n] &#124; All}-c&#124;ServerConnection <servidor-Connection-File> [-v&#124;Variable <variável-value-File>] [-o/overwrite]<br /><br />ou o<br /><br />-a/adicionar {<server_id> [,... n] &#124; todos os}-s&#124;script <script-arquivo> [-v&#124;variável <variável-valor-arquivo>] [-o/substituir]<br /><br />-r/remover {<server_id> [,... n] &#124; todos}<br /><br />-l/lista<br /><br />-e/exportar {<Server-ID> [,... n] &#124; todos} <arquivo criptografado-senha><br /><br />-i/Import {<Server-ID> [,... n] &#124; todos} <arquivo criptografado-senha>|Se especificado, essa opção não deve ser combinada com nenhuma outra opção.<br /><br />Server-ID: uma ID exclusiva fornecida para um servidor {String}<br /><br />servidor-arquivo de conexão: arquivo de definição de servidor (serverconnectionfile ou scriptfile).<br /><br />variável-de-valor-arquivo: é um arquivo de definição de variável e usado no arquivo de conexão de servidor.<br /><br />Encrypt-password-file: é um arquivo de senhas de servidor criptografado usando uma frase secreta especificada pelo usuário.|  
|8|-?|Não|Não Aplicável|Não Aplicável|  
  
## <a name="see-also"></a>Consulte Também  
[Executando o console do SSMA (Sybase)](https://msdn.microsoft.com/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
