---
title: Opções de linha de comando no Console do SSMA (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c1f3b3f0-0f3e-4e07-b745-2fbdde85c67e
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: fc8065bcfda3066fae31be982e25f054c07bca3a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62650760"
---
# <a name="command-line-options-in-the-ssma-console-accesstosql"></a>Opções de linha de comando no Console do SSMA (AccessToSQL)
Microsoft fornece um conjunto robusto de opções de linha de comando para executar e controlar atividades do SSMA. Seções a seguir fornecem mais detalhes.  
  
## <a name="command-line-options-in-the-ssma-console"></a>Opções de linha de comando no Console do SSMA  
Descritos aqui é o console de opções de comando.  
  
Para fins desta seção, o termo 'option' também é conhecido como 'switch'.  
  
As opções não diferenciam maiusculas de minúsculas e pode começar com o '**-**'ou'**/**' caracteres.  
  
Se as opções forem especificadas, é obrigatório que você especifique os parâmetros de opção correspondente.  
  
Parâmetros de opção devem ser separados do caractere opção por espaço em branco.  
  
**Exemplos de sintaxe:**  
  
`C:\> SSMAforAccessConsole.EXE -s scriptfile`  
  
`C:\> SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\VariableValueFileSample.xml" -c "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml"`  
  
Nomes de arquivo ou pasta que contém espaços devem ser especificados entre aspas duplas.  
  
A saída de mensagens de erro e entradas de linha de comando é armazenada em STDOUT ou em um arquivo especificado.  
  
### <a name="script-file-option--sscript"></a>Opção de arquivo de script: -s/script  
Uma opção obrigatória, o caminho/nome de arquivo de script Especifica o script de sequências de comando a ser executado pelo SSMA.  
  
**Exemplos de sintaxe:**  
  
`C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"`  
  
### <a name="variable-value-file-option--vvariable"></a>Opção de arquivo do valor da variável: - v/variável  
O arquivo de valor da variável é composto de variáveis usadas no arquivo de script. A opção é opcional. Se as variáveis não são declaradas no arquivo de variável e usadas no arquivo de script, o aplicativo gera um erro e finaliza a execução do console.  
  
**Exemplos de sintaxe:**  
  
-   Variáveis definidas em vários arquivos de valor da variável, talvez um com um valor padrão e outro com um valor específico da instância quando aplicável. O último arquivo de variável especificado nos argumentos de linha de comando leva a preferência, caso haja uma eliminação de duplicação de variáveis:  
  
    `C:\>SSMAforAccessConsole.EXE -s`  
  
    `"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml" -v c:\migration`  
  
    `projects\global_variablevaluefile.xml -v "c:\migrationprojects\instance_variablevaluefile.xml"`  
  
### <a name="server-connection-file-option--cserverconnection"></a>Opção de arquivo de conexão do servidor: - c/serverconnection  
Esse arquivo contém informações de conexão do servidor para cada servidor. Cada definição de servidor é identificada por uma ID de servidor única. As IDs do servidor são referenciadas no arquivo de script para os comandos relacionados à conexão.  
  
Definição de servidor pode ser uma parte do arquivo de conexão do servidor e/ou o arquivo de script. Id do servidor no arquivo de script tem precedência sobre o arquivo de conexão de servidor, caso haja uma duplicação da id do servidor.  
  
**Exemplos de sintaxe:**  
  
-   As IDs do servidor são usadas no arquivo de script. Eles são definidos em um arquivo de conexão de servidor separado. Este arquivo usa variáveis que são definidas no arquivo de valor da variável:  
  
    `C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -v`  
  
    `c:\SsmaProjects\myvaluefile1.xml -c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   Definição de servidor é inserida no arquivo de script:  
  
    `C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>Opção de saída de XML: - x / xmloutput [xmloutputfile]  
Esse comando é usado para gerar as mensagens de saída do comando em um formato xml para o console ou em um arquivo xml.  
  
Há duas opções disponíveis para xmloutput, ou seja:  
  
-   Se o caminho do arquivo é fornecido após a opção xmloutput, a saída é redirecionada para o arquivo.  
  
    **Exemplo de sintaxe:**  
  
    `C:\>SSMAforAccessConsole.EXE -s`  
  
    `"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -x d:\xmloutput\project1output.xml`  
  
-   Se nenhum caminho de arquivo é fornecido após a opção xmloutput, o xmlout é exibido no console em si.  
  
    **Exemplo de sintaxe:**  
  
    `C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -xmloutput`  
  
### <a name="log-file-option--llog"></a>Opção de arquivo de log: -l/log  
Todas as operações no aplicativo de Console SSMA são registradas em um arquivo de log, e a opção é opcional. Se um arquivo de log e seu caminho são especificados na linha de comando, o log é gerado no local especificado. Caso contrário, ele é gerado em seu local padrão.  
  
**Exemplo de sintaxe:**  
  
`C:\>SSMAforAccessConsole.EXE`  
  
`"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option--eprojectenvironment"></a>Opção de pasta de ambiente do projeto: - a e/projectenvironment  
Esta opção indica que a pasta de configurações do ambiente de projeto para o projeto atual do SSMA.  
  
**Exemplo de sintaxe:**  
  
`C:\>SSMAforAccessConsole.EXE -s`  
  
`"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -e c:\SsmaProjects\CommonEnvironment`  
  
||  
|-|  
||  
  
### <a name="secure-password-option--psecurepassword"></a>Proteger a opção de senha: -p/securepassword  
Esta opção indica que a senha criptografada para conexões de servidor. Ele difere de todas as outras opções em que ele não executar qualquer script ou Ajuda em todas as atividades relacionadas à migração, mas ajuda a gerenciar a criptografia de senha para as conexões de servidor usado no projeto de migração.  
  
Você não pode inserir qualquer outra opção ou senha como o parâmetro de linha de comando. Caso contrário, ele resulta em um erro. Para obter mais informações, consulte o [gerenciamento de senhas](managing-passwords-accesstosql.md) seção.  
  
As subopções a seguir têm suporte para `-p/securepassword`:  
  
-   Para adicionar uma senha ou atualizar uma senha existente, para o armazenamento protegido para uma ID do servidor especificado ou para todas as IDs de servidor definido no arquivo de conexão do servidor:  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
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
  
### <a name="help-option--help"></a>Opção de Ajuda:-? /help  
Exibe o resumo de sintaxe de opções do Console do SSMA:  
  
`C:\>SSMAforAccessConsole.EXE -?`  
  
Para obter uma exibição tabular das opções de linha de comando de Console do SSMA, consulte [Apêndice – 1 &#40;AccessToSQL&#41;](../../ssma/access/appendix-1-accesstosql.md).  
  
### <a name="securepassword-help-option--securepassword--help"></a>A opção de ajuda de SecurePassword: - securepassword-? /Help  
Exibe o resumo de sintaxe de opções do Console do SSMA:  
  
`C:\>SSMAforAccessConsole.EXE -securepassword -?`  
  
Para obter uma exibição tabular das opções de linha de comando de Console do SSMA, consulte [Apêndice – 1 &#40;AccessToSQL&#41;](../../ssma/access/appendix-1-accesstosql.md)  
  
### <a name="next-steps"></a>Próximas etapas  
A próxima etapa depende de seus requisitos de projeto:  
  
1.  Para especificar uma senha ou a exportação / importação de senhas, consulte [gerenciamento de senhas &#40;AccessToSQL&#41;](../../ssma/access/managing-passwords-accesstosql.md).  
  
2.  Para gerar relatórios, consulte [geração de relatórios &#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md).  
  
3.  Para solucionar problemas no console, consulte [solução de problemas &#40;AccessToSQL&#41;](../../ssma/access/troubleshooting-accesstosql.md).  
  
