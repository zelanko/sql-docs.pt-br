---
title: "Opções de linha de comando no Console do SSMA (AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 08/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c1f3b3f0-0f3e-4e07-b745-2fbdde85c67e
caps.latest.revision: "11"
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: Inactive
ms.openlocfilehash: af93a39eb16c45de0e848bc7b41cdf2758bd1ae0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="command-line-options-in-the-ssma-console-accesstosql"></a>Opções de linha de comando no Console do SSMA (AccessToSQL)
Microsoft fornece um conjunto robusto de opções de linha de comando para executar e controlar as atividades do SSMA. As seções resultantes fornecem detalhes adicionais.  
  
## <a name="command-line-options-in-the-ssma-console"></a>Opções de linha de comando no Console do SSMA  
Aqui descritos é o console de opções de comando.  
  
Para fins desta seção, o termo 'option' também é conhecido como 'switch'.  
  
Opções não diferenciam maiusculas de minúsculas e pode começar com o '**-**'ou'**/**' caracteres.  
  
Se forem especificadas opções, é obrigatório que você especifique os parâmetros de opção correspondentes.  
  
Parâmetros de opção devem ser separados de caractere a opção por espaço em branco.  
  
**Exemplos de sintaxe:**  
  
`C:\> SSMAforAccessConsole.EXE -s scriptfile`  
  
`C:\> SSMAforAccessConsole.EXE -s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml” –v “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\VariableValueFileSample.xml” –c “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml”`  
  
Nomes de arquivo ou pasta contendo espaços devem ser especificados entre aspas duplas.  
  
A saída de mensagens de erro e entradas de linha de comando é armazenada em STDOUT ou em um arquivo especificado.  
  
### <a name="script-file-option-sscript"></a>Opção de arquivo de script: – s/script  
Quando a opção é obrigatória, o caminho/nome de arquivo de script Especifica o script de sequências de comando a ser executado pelo SSMA.  
  
**Exemplos de sintaxe:**  
  
`C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”`  
  
### <a name="variable-value-file-option-vvariable"></a>Opção de arquivo de valor da variável: – v/variável  
O arquivo de valor de variável consiste em variáveis usadas no arquivo de script. A opção é opcional. Se as variáveis não são declaradas no arquivo de variável e usadas no arquivo de script, o aplicativo gera um erro e termina a execução do console.  
  
**Exemplos de sintaxe:**  
  
-   Variáveis definidas em vários arquivos de valor da variável, talvez uma com um valor padrão e outra com um valor específico da instância quando aplicável. O último arquivo de variável especificado nos argumentos de linha de comando usa a preferência, caso haja uma eliminação de duplicação de variáveis:  
  
    `C:\>SSMAforAccessConsole.EXE -s`  
  
    `“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml” –v c:\migration`  
  
    `projects\global_variablevaluefile.xml –v “c:\migrationprojects\instance_variablevaluefile.xml”`  
  
### <a name="server-connection-file-option-cserverconnection"></a>Opção de arquivo de conexão de servidor: – c/serverconnection  
Esse arquivo contém informações de conexão de servidor para cada servidor. Cada definição de servidor é identificada por uma ID de servidor exclusivo. As IDs de servidor são referenciadas no arquivo de script de comandos relacionados à conexão.  
  
Definição de servidor pode ser uma parte do arquivo de conexão de servidor e/ou o arquivo de script. Identificação do servidor de arquivo de script tem precedência sobre o arquivo de conexão de servidor, caso haja uma eliminação de duplicação de identificação do servidor.  
  
**Exemplos de sintaxe:**  
  
-   As IDs do servidor são usadas no arquivo de script. Eles são definidos em um arquivo de conexão de servidor separado. Esse arquivo usa as variáveis definidas no arquivo de valor da variável:  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –v`  
  
    `c:\SsmaProjects\myvaluefile1.xml –c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   Definição de servidor é inserida no arquivo de script:  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>Opção de saída de XML: - x / xmloutput [xmloutputfile]  
Esse comando é usado para gerar as mensagens de saída do comando em um formato xml para o console ou em um arquivo xml.  
  
Há duas opções disponíveis para xmloutput, ou seja:  
  
-   Se o caminho do arquivo é fornecido após a opção xmloutput, a saída é redirecionada para o arquivo.  
  
    **Exemplo de sintaxe:**  
  
    `C:\>SSMAforAccessConsole.EXE –s`  
  
    `“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –x d:\xmloutput\project1output.xml`  
  
-   Se nenhum caminho de arquivo é fornecido após a opção xmloutput, o xmlout é exibido no console em si.  
  
    **Exemplo de sintaxe:**  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –xmloutput`  
  
### <a name="log-file-option-llog"></a>Opção de arquivo de log: – l/log  
Todas as operações no aplicativo do Console SSMA são registradas em um arquivo de log, e a opção é opcional. Se um arquivo de log e o caminho for especificados na linha de comando, o log é gerado no local especificado. Caso contrário, ele obtém gerado em seu local padrão.  
  
**Exemplo de sintaxe:**  
  
`C:\>SSMAforAccessConsole.EXE`  
  
`“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option-eprojectenvironment"></a>Opção de pasta de ambiente do projeto: – e/projectenvironment  
Esta opção indica que a pasta de configurações do ambiente de projeto para o projeto atual do SSMA.  
  
**Exemplo de sintaxe:**  
  
`C:\>SSMAforAccessConsole.EXE –s`  
  
`“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –e c:\SsmaProjects\CommonEnvironment`  
  
||  
|-|  
||  
  
### <a name="secure-password-option-psecurepassword"></a>Opção de senha de segurança: – p/securepassword  
Esta opção indica que a senha criptografada para conexões de servidor. Ele difere de todas as outras opções não executar qualquer script ou ajudá-lo em todas as atividades relacionadas à migração, mas ajuda a gerenciar a criptografia de senha para as conexões de servidor usada no projeto de migração.  
  
Você não pode inserir qualquer outra opção ou senha como o parâmetro de linha de comando. Caso contrário, isso resulta em erro. Para obter mais informações, consulte o [gerenciar senhas](http://msdn.microsoft.com/b099d0f9-dd37-4c87-8b6f-ed0177881ea4) seção.  
  
As subopções a seguir têm suporte para `–p/securepassword`:  
  
-   Para adicionar uma senha ou atualizar uma senha existente, o armazenamento protegido para uma ID especificada do servidor ou para todas as IDs de servidor definido no arquivo de conexão do servidor:  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   Para remover a senha criptografada do armazenamento protegido da ID especificada do servidor ou para todas as IDs do servidor:  
  
    `–p/securepassword –r/remove {<server_id> [, …n] | all}`  
  
-   Para exibir uma lista de IDs de servidor para o qual a senha é criptografada:  
  
    `–p/securepassword –l/list`  
  
-   Para exportar as senhas armazenadas no armazenamento protegido para um arquivo criptografado. Esse arquivo é criptografado com a frase secreta especificada pelo usuário.  
  
    `–p/securepassword –e/export {<server-id> [, …n] | all} <encrypted-password -file>`  
  
-   O criptografado-arquivo que foi exportado anteriormente é importado para o armazenamento protegido local usando a frase secreta especificada pelo usuário. Depois que o arquivo for descriptografado, ela será armazenada em um novo arquivo, que por sua vez, é criptografado no computador local.  
  
    `–p/securepassword –i/import {<server-id> [, …n] | all} <encrypted-password -file>`  
  
    Várias IDs de servidor podem ser especificadas usando separadores de vírgula.  
  
### <a name="help-option-help"></a>Opção de Ajuda: –? /help  
Exibe o resumo da sintaxe de opções do Console do SSMA:  
  
`C:\>SSMAforAccessConsole.EXE -?`  
  
Para obter uma exibição tabular das opções de linha de comando do Console SSMA, consulte [apêndice a-1 &#40; AccessToSQL &#41; ](../../ssma/access/appendix-1-accesstosql.md).  
  
### <a name="securepassword-help-option-securepassword--help"></a>Opção SecurePassword ajuda: – securepassword-? /Help  
Exibe o resumo da sintaxe de opções do Console do SSMA:  
  
`C:\>SSMAforAccessConsole.EXE -securepassword -?`  
  
Para obter uma exibição tabular das opções de linha de comando do Console SSMA, consulte [apêndice a-1 &#40; AccessToSQL &#41;](../../ssma/access/appendix-1-accesstosql.md)  
  
### <a name="next-steps"></a>Próximas etapas  
A próxima etapa depende de seus requisitos de projeto:  
  
1.  Para especificar uma senha ou a exportação / importação de senhas, consulte [gerenciar senhas &#40; AccessToSQL &#41; ](../../ssma/access/managing-passwords-accesstosql.md).  
  
2.  Para gerar relatórios, consulte [gerando relatórios &#40; AccessToSQL &#41; ](../../ssma/access/generating-reports-accesstosql.md).  
  
3.  Para solucionar problemas no console, consulte [solução de problemas &#40; AccessToSQL &#41; ](../../ssma/access/troubleshooting-accesstosql.md).  
  
