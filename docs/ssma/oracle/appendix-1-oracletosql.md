---
description: Apêndice – 1 (OracleToSQL)
title: Apêndice-1 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e01f8be5-ce68-4c9f-bd13-d65e73a16470
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: db1b6f9c7dc71bec58dd101f2fa7cb9f30f7f7ce
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037379"
---
# <a name="appendix---1-oracletosql"></a>Apêndice – 1 (OracleToSQL)
Exibição rápida das opções de linha de comando do console do SSMA:  
  
|SL. Não.|Alternar|Necessário?|Argumento de opção|Valores permitidos|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sim|scriptfile|Nome de arquivo XML válido.<br /><br />Arquivo de definição de script do console.|  
|2|-v/variável|No|variablevaluefile|Nome de arquivo XML válido.<br /><br />Se forem usadas variáveis no arquivo de script, esse arquivo deverá ser especificado.|  
|3|-c/ServerConnection|No|serverconnectionfile|Nome de arquivo XML válido.<br /><br />Esse arquivo contém informações de conexão do servidor.|  
|4|-x/xmloutput|No|xmlarquivo_de_saída|Essa opção indica a saída do console no formato XML. Se essa opção não for especificada, a saída padrão estará no formato de texto.<br /><br />Se xmloutputtypefile não for especificado, a saída XML será direcionada para `STDOUT` .<br /><br />Xmloutputtype é o nome do arquivo no qual a saída do console é gravada no formato XML.|  
|5|-l/log|No|logfile|Nome de arquivo válido.|  
|6|-e/projectenvironment|No|projectenvironmentfolder|Nome de pasta válido que contém arquivos de ambiente do projeto do SSMA.|  
|7|-p/SecurePassword|No|-a/adicionar {<server_id> [,... n] &#124; All}-c&#124;ServerConnection <servidor-Connection-File> [-v&#124;Variable <variável-value-File>] [-o/overwrite]<br /><br />ou<br /><br />-a/adicionar {<server_id> [,... n] &#124; todos os}-s&#124;script <script-arquivo> [-v&#124;variável <variável-valor-arquivo>] [-o/substituir]<br /><br />-r/remover {<server_id> [,... n] &#124; todos}<br /><br />-l/lista<br /><br />-e/exportar {<Server-ID> [,... n] &#124; todos} <arquivo criptografado-senha><br /><br />-i/Import {<Server-ID> [,... n] &#124; todos} <arquivo criptografado-senha>|Se especificado, essa opção não deve ser combinada com nenhuma outra opção.<br /><br />Server-ID: uma ID exclusiva fornecida para um servidor {String}<br /><br />servidor-arquivo de conexão: arquivo de definição de servidor (serverconnectionfile ou scriptfile).<br /><br />variável-de-valor-arquivo: é um arquivo de definição de variável e usado no arquivo de conexão de servidor.<br /><br />Encrypt-password-file: é um arquivo de senhas de servidor criptografado usando uma frase secreta especificada pelo usuário.|  
|8|-?|No|Não Aplicável|Não Aplicável|  
  
## <a name="see-also"></a>Consulte Também  
[Executando o console do SSMA (Oracle)](./executing-the-ssma-console-oracletosql.md)  
