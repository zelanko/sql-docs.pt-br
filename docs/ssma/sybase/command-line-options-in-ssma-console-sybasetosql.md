---
title: Opções de linha de comando no Console do SSMA (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Command Line Options
ms.assetid: 337cbd26-67b7-4c88-9deb-d0a69a3d7714
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 285f5c58c94db0f5506f84d19c992dfcdbbd00d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083481"
---
# <a name="command-line-options-in-ssma-console-sybasetosql"></a>Opções de linha de comando no Console do SSMA (SybaseToSQL)
Microsoft fornece um conjunto robusto de opções de linha de comando para executar e controlar atividades do SSMA. Seções a seguir detalham os mesmos.  
  
## <a name="command-line-options-in-ssma-console"></a>Opções de linha de comando no Console do SSMA  
Descritos aqui é o console de opções de comando.  
  
Para fins desta seção, o termo 'option' também é conhecido como 'switch'.  
  
-   As opções não diferenciam maiusculas de minúsculas e pode começar com ' **-** 'ou', **/** ' caracteres.  
  
-   Se as opções forem especificadas, se torna obrigatório especificar os parâmetros de opção correspondente.  
  
-   Parâmetros de opção devem ser separados do caractere opção por espaço em branco.  
  
    **Exemplos de sintaxe:**  
  
    `C:\> SSMAforSybaseConsole.EXE -s scriptfile`  
  
    `C:\> SSMAforSybaseConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\VariableValueFileSample.xml" -c "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ServersConnectionFileSample.xml"`  
  
-   Nomes de arquivo ou pasta que contém espaços devem ser especificados entre aspas duplas.  
  
-   A saída de entradas de linha de comando e mensagens de erro são armazenados em STDOUT ou em um arquivo especificado.  
  
### <a name="script-file-option--sscript"></a>Opção de arquivo de script: -s/script  
Uma opção obrigatória, o caminho/nome de arquivo de script Especifica o script de sequências de comando a ser executado pelo SSMA.  
  
**Exemplos de sintaxe:**  
  
`C:\>SSMAforSybaseConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"`  
  
### <a name="variable-value-file-option--vvariable"></a>Opção de arquivo de valor variável: - v/variável  
Esse arquivo é composto de variáveis usadas no arquivo de script. Isso é uma opção facultativa. Se as variáveis não são declaradas no arquivo de variável e usadas no arquivo de script, o aplicativo gera um erro e finaliza a execução do console.  
  
**Exemplos de sintaxe:**  
  
-   Variáveis definidas em vários arquivos de valor da variável, talvez um com um valor padrão e outro com um valor específico de instância quando aplicável. O último arquivo de variável especificado nos argumentos de linha de comando leva a preferência, caso haja uma eliminação de duplicação de variáveis:  
  
    `C:\>SSMAforSybaseConsole.EXE -s`  
  
    `"C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml" -v c:\migration`  
  
    `projects\global_variablevaluefile.xml -v "c:\migrationprojects\instance_variablevaluefile.xml"`  
  
### <a name="server-connection-file-option--cserverconnection"></a>Opção de arquivo de Conexão de servidor: -c/serverconnection  
Esse arquivo contém informações de conexão do servidor para cada servidor. Cada definição de servidor é identificada por uma ID de servidor única. As IDs do servidor são referenciadas no arquivo de script para conexão comandos relacionados.  
  
Definição de servidor pode ser uma parte do arquivo de conexão do servidor e/ou o arquivo de script. Id do servidor no arquivo de script tem precedência sobre o arquivo de conexão de servidor, caso haja uma duplicação da id do servidor.  
  
**Exemplos de sintaxe:**  
  
-   As IDs do servidor são usadas no arquivo de script e eles são definidos em um arquivo de conexão de servidor separado, arquivo de conexão de servidor usa as variáveis que são definidas no arquivo de valor da variável:  
  
    `C:\>SSMAforSybaseConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -v`  
  
    `c:\SsmaProjects\myvaluefile1.xml -c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   Definição de servidor é inserida no arquivo de script:  
  
    `C:\>SSMAforSybaseConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>Opção de saída XML: - x / xmloutput [xmloutputfile]  
Esse comando é usado para gerar as mensagens de saída do comando em um formato xml para o console ou em um arquivo xml.  
  
Há duas opções disponíveis para xmloutput, sobre visualização..,:  
  
-   Se o caminho do arquivo é fornecido após a opção xmloutput a saída é redirecionada para o arquivo.  
  
    **Exemplo de sintaxe:**  
  
    `C:\>SSMAforSybaseConsole.EXE -s`  
  
    `"C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -x d:\xmloutput\project1output.xml`  
  
-   Se nenhum caminho de arquivo é fornecido após a opção xmloutput o xmlout é exibido no console em si.  
  
    **Exemplo de sintaxe:**  
  
    `C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -xmloutput`  
  
### <a name="log-file-option--llog"></a>Opção de arquivo de log: -l/log  
Todas as operações no aplicativo de Console SSMA obterem registradas em um arquivo de log. Isso é uma opção facultativa. Se um arquivo de log e seu caminho são especificados na linha de comando, o log é gerado no local especificado. Caso contrário, ele é gerado em seu local padrão.  
  
**Exemplo de sintaxe:**  
  
`C:\>SSMAforSybaseConsole.EXE`  
  
`"C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option--eprojectenvironment"></a>Opção de pasta do ambiente de projeto: - a e/projectenvironment  
Isso indica que a pasta de configurações do ambiente de projeto para o projeto atual do SSMA. Essa opção é opcional.  
  
**Exemplo de sintaxe:**  
  
`C:\>SSMAforSybaseConsole.EXE -s`  
  
`"C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -e c:\SsmaProjects\CommonEnvironment`  
  
### <a name="secure-password-option--psecurepassword"></a>Opção de senha segura: -p/securepassword  
Esta opção indica que a senha criptografada para conexões de servidor. Ele é diferente de todas as outras opções: a opção não executa qualquer script nem ajuda em todas as atividades relacionadas à migração, mas ajuda a gerenciar a criptografia de senha para as conexões de servidor usado no projeto de migração.  
  
Você não pode inserir qualquer outra opção ou senha como o parâmetro de linha de comando. Caso contrário, ele resulta em um erro. Para obter mais informações, consulte o [gerenciamento de senhas](managing-passwords-sybasetosql.md) seção.  
  
As seguintes opções subsistema têm suporte para `-p/securepassword`:  
  
-   Para adicionar a senha para armazenamento protegido para uma ID do servidor especificado ou para todas as IDs de servidor definido no arquivo de conexão do servidor. -Substitui a opção abaixo, as atualizações a senha se ela já existir:  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}` `-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   Para remover a senha criptografada do armazenamento protegido da ID especificada do servidor ou para todas as IDs do servidor:  
  
    `-p/securepassword -r/remove {<server_id> [, ...n] | all}`  
  
-   Para exibir uma lista de IDs de servidor para o qual a senha é criptografada:  
  
    `-p/securepassword -l/list`  
  
-   Para exportar as senhas armazenadas no armazenamento protegido para um arquivo criptografado. Esse arquivo é criptografado com a frase secreta especificada pelo usuário.  
  
    `-p/securepassword -e/export {<server-id> [, ...n] | all} <encrypted-password -file>`  
  
-   O criptografado-arquivo que foi exportado anteriormente é importado para o armazenamento protegido local usando a frase secreta especificada pelo usuário. Depois que o arquivo é descriptografado, ela é armazenada em um novo arquivo, por sua vez, é criptografado no computador local.  
  
    `-p/securepassword -i/import {<server-id> [, ...n] | all} <encrypted-password -file>`  
  
    Várias IDs do servidor pode ser especificadas usando os separadores de vírgula.  
  
### <a name="help-option--help"></a>A opção de Ajuda:-? /help  
Exibe o resumo de sintaxe de opções do Console do SSMA:  
  
`C:\>SSMAforSybaseConsole.EXE -?`  
  
Para obter uma exibição tabular das opções de linha de comando do Console do SSMA, consulte [Apêndice – 1 &#40;SybaseToSQL&#41;](../../ssma/sybase/appendix-1-sybasetosql.md).  
  
### <a name="securepassword-help-option--securepassword--help"></a>A opção de ajuda de SecurePassword: - securepassword-? /Help  
Exibe o resumo de sintaxe de opções do Console do SSMA:  
  
`C:\>SSMAforSybaseConsole.EXE -securepassword -?`  
  
Para obter uma exibição tabular das opções de linha de comando do Console do SSMA, consulte [Apêndice – 1 &#40;SybaseToSQL&#41;](../../ssma/sybase/appendix-1-sybasetosql.md)  
  
### <a name="next-step"></a>Próxima etapa  
A próxima etapa depende de seus requisitos de projeto:  
  
-   Para especificar uma senha ou a exportação / importação de senhas, consulte [gerenciamento de senhas &#40;SybaseToSQL&#41;](../../ssma/sybase/managing-passwords-sybasetosql.md).  
  
-   Para gerar relatórios, consulte [geração de relatórios &#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md).  
  
-   Para solucionar problemas no console, consulte [solução de problemas &#40;SybaseToSQL&#41;](../../ssma/sybase/troubleshooting-sybasetosql.md).  
  
