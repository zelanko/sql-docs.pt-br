---
title: Erros conhecidos e soluções com o Change Data Capture para Oracle da Attunity | Microsoft Docs
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ee1e8f3ae65b4a906d42a4b00644456d89f9b900
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71713421"
---
# <a name="known-errors-and-resolutions-with-change-data-capture-for-oracle-by-attunity"></a>Erros conhecidos e soluções com o Change Data Capture para Oracle da Attunity
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdbmi-xxxx-xxx-md.md)]

Este tópico lista os principais problemas e as soluções conhecidas ao exibir uma instância da CDA (captura de dados de alterações) na ferramenta de configuração do Oracle CDC Designer. Essa ferramenta faz parte do Change Data Capture para Oracle da Attunity que está incluída do SQL Server 2012 em diante. 

## <a name="bug-fixes"></a>Correções de bug
Antes de gastar muito tempo Solucionando problemas, é importante usar os builds mais recentes da CDA para Oracle da Attunity para evitar problemas conhecidos, tais como estes:

### <a name="sql-server-2017"></a>Microsoft SQL Server 2017

A **versão 5.0.0.111** contém estas correções:
- Correção de bug – o Oracle CDC Designer falha com "Sintaxe incorreta próxima à palavra-chave 'KEY'" ao adicionar uma tabela do Oracle. 
- Melhoria – suporte aprimorado para RAC, isso inclui melhor manipulação quando um nó do RAC é reiniciado. 
- Correção de bug – a CDA não está funcionando com o Oracle 10.2 devido à solicitação de NEXT_CHANGE# do v$log. 


A **versão 5.0.0.93** contém estas correções: 
- O Microsoft CDC Designer para Oracle da Attunity falha com o erro "Sintaxe incorreta próxima à palavra 'KEY'" ao adicionar uma tabela do Oracle. 

 
### <a name="sql-server-2016"></a>SQL Server 2016

A **versão 4.0.107** contém estas correções:
- Correções de bug – o Oracle CDC Designer falha com "Sintaxe incorreta próxima à palavra-chave 'KEY'" ao adicionar uma tabela do Oracle.
- Melhoria – suporte aprimorado para RAC, isso inclui melhor manipulação quando um nó do RAC é reiniciado.
- Correções de bug – a CDA não está funcionando com o Oracle 10.2 devido à solicitação de NEXT_CHANGE# do v$log.

A **versão 4.0.0.95** contém estas correções: 
- Correções de bug – o Oracle CDC Designer falha com "Sintaxe incorreta próxima à palavra-chave 'KEY'" ao adicionar uma tabela do Oracle.

A **versão 4.0.0.88** contém estas correções:
-  As propriedades adicionadas nas opções avançadas da instância da CDA da Attunity são removidas quando uma tabela é adicionada ou removida da CDA. 
- A CDA da Attunity para de funcionar após a aplicação da correção do SQL que adiciona a coluna __$command_id

### <a name="sql-server-2014"></a>SQL Server 2014 

A **versão 2.0.0.114** contém estas correções:
- Correções de bug – o Oracle CDC Designer falha com "Sintaxe incorreta próxima à palavra-chave 'KEY'" ao adicionar uma tabela do Oracle.
- Melhoria – suporte aprimorado para RAC, isso inclui melhor manipulação quando um nó do RAC é reiniciado.
- Correções de bug – a CDA não está funcionando com o Oracle 10.2 devido à solicitação de NEXT_CHANGE# do v$log.

A **versão 2.0.0.92** contém estas correções: 
- As propriedades adicionadas nas opções avançadas da instância da CDA da Attunity são removidas quando uma tabela é adicionada ou removida da CDA. A CDA da Attunity para de funcionar após a aplicação da correção do SQL que adiciona a coluna __$command_id
- Falha na validação de metadados para a tabela do Oracle cdc.table_name. O índice da coluna column_name está fora do intervalo.  E este problema: O serviço Oracle CDC mostra o status anulado quando você usa a CDA para Oracle da Attunity
    - Corrigido na _Atualização cumulativa 1 para SQL Server 2014 RTM_, conforme descrito em KB [2894025](https://support.microsoft.com/kb/2894025).
- Algumas alterações são perdidas e não são replicadas para o banco de dados do SQL Server. Esse problema ocorre quando uma tabela contém mais de um CLOB (objeto binário grande de caractere) e um dos CLOBs tem um valor grande. 
    - Corrigido na _Atualização cumulativa 1 para SQL Server 2014 SP1_ e _Atualização cumulativa 8 para SQL Server 2014 RTM_, conforme descrito em KB [3029096](https://support.microsoft.com/kb/3029096). 
- O Change Data Capture para Oracle da Attunity para de funcionar quando as tabelas Oracle têm uma coluna com o tipo de dados Long.
    - Corrigido na _Atualização cumulativa 5 para SQL Server 2014 SP1_ e _Atualização cumulativa 12 para SQL 2014 RTM_, conforme descrito em KB [3145983](https://support.microsoft.com/kb/3145983).

### <a name="sql-server-2012"></a>SQL Server 2012

A **versão 1.1.0.102** contém estas correções: 
 
- As propriedades adicionadas nas opções avançadas da instância da CDA da Attunity são removidas quando uma tabela é adicionada ou removida da CDA. A CDA da Attunity para de funcionar após a aplicação da correção do SQL que adiciona a coluna __$command_id
- A instância da CDA para Oracle trava quando você a inicia e não captura alterações. A memória do servidor da Oracle pode aumentar até que ele fique sem memória ou falhe.
- [2672759](https://support.microsoft.com/kb/2672759): Mensagem de erro quando você usa o Serviço Microsoft Change Data Capture para Oracle da Attunity: "ORA-00600: código de erro interno". Adicione o rastreamento de nível SOURCE e confirme se você encontra o mesmo erro ORA-00600. Corrigido por um download de patch do Oracle.
- Várias partições
    - Quando você usa mais de 10 partições em uma tabela do Oracle, a instância da CDA não pode capturar todas as alterações da tabela. Quando a tabela do Oracle é definida com mais de 10 partições, são capturadas somente as alterações das últimas 10 partições. Corrigido na versão _Service Pack 1 para SQL Server 2012_. Confira a [página de download do SP1 Feature Pack](https://www.microsoft.com/download/details.aspx?id=35580). 
- As alterações são perdidas
    - A captura de eventos pode entrar em um loop infinito e interromper a captura de novas alterações de dados (relacionado ao bug 5623813 do Oracle). Quando um ambiente RAC do Oracle está executando uma interrupção ou retomada da instância da CDA, as alterações podem ser ignoradas/perdidas. Isso significa que o Change Data Capture do SQL Server não terá linhas importantes e, portanto, haverá perda de dados no sistema de data warehouse ou no sistema assinante. Corrigido na versão _Service Pack 1 para SQL Server 2012_. Confira a [página de download do SP1 Feature Pack](https://www.microsoft.com/download/details.aspx?id=35580)
- Larguras duplas em colunas no SQL
    - Ao criar uma instância da CDA para Oracle, nos scripts a serem executados no SQL Server, o comprimento de uma coluna de tipo de dados de largura variável é duplicado em tabelas do SQL Server criadas no script. Por exemplo, se você tentar controlar as alterações em uma coluna VARCHAR2(10) em uma tabela do Oracle, a coluna correspondente na tabela SQL Server será NVARCHAR(20) no script de implantação. Corrigido em qualquer das seguintes atualizações: _Atualização cumulativa 2 para SQL Server 2012 SP1_ e _Atualização cumulativa 5 para SQL Server 2012_, conforme descrito em KB [2769673](https://support.microsoft.com/kb/2769673). 
- Os dados da DDL estão truncados
    - Quando você executa uma instrução DDL (linguagem de definição de dados) que tem mais de 4.000 bytes em um Oracle Database que contém caracteres não latinos, a CDA para Oracle da Attunity falha. Além disso, você vê a mensagem de erro `ORA-01406: fetched column value was truncated.`. Corrigido na _Atualização cumulativa 4 para SQL Server 2012 SP1_, conforme descrito em KB [2839806](https://support.microsoft.com/kb/2839806). 
- As alterações são perdidas nas duas últimas colunas
    - Corrigido na _Atualização cumulativa 6 para SQL Server 2012 SP1_, conforme descrito em KB [2874879](https://support.microsoft.com/kb/2874879). 
- O log de transações do SQL cresce quando você usa a CDA para Oracle
     - Quando as instâncias do Change Data Capture para Oracle forem configuradas, o Banco de Dados SQL que recebe os dados alterados terá tabelas espelhadas, com transações marcadas para replicação. Esse comportamento ocorre porque a CDA para Oracle depende de procedimentos armazenados do sistema subjacente semelhantes aos usados na CDA para SQL Server. No entanto, como não há nenhuma replicação da CDA para SQL envolvida quando a CDA para Oracle é usado sozinho, não há nenhum leitor de log para limpar as transações que estão marcadas para replicação. Já que a transação não precisa ser replicada no SQL Server, é seguro marcar manualmente a transação como distribuída usando a solução alternativa descrita posteriormente neste artigo. Mais informações podem ser encontradas em KB [2871474](https://support.microsoft.com/kb/2871474). 
- Erro `ORACDC000T: Error encountered at position to change event - SCN not found - EOF simulated`. Corrigido na _Atualização cumulativa 7 para SQL Server 2012 SP1_, conforme descrito em KB [2883524](https://support.microsoft.com/kb/2883524). 
- Falha na validação de metadados para a tabela do Oracle cdc.table_name. O índice da coluna column_name está fora do intervalo. Corrigido na _Atualização cumulativa 7 para SQL Server 2012 SP1_, conforme descrito em KB [2883524](https://support.microsoft.com/kb/2883524).
- O serviço Oracle CDC mostra o status anulado quando você usa a CDA para Oracle da Attunity no SQL Server 2012. Corrigido na _Atualização cumulativa 8 para SQL Server 2012 SP1_, conforme descrito em KB [2923839](https://support.microsoft.com/kb/2923839).  
- Algumas alterações são perdidas e não são replicadas para os bancos de dados do SQL Server. Esse problema ocorre quando uma tabela contém mais de um CLOB (objeto binário grande de caractere) e um dos CLOBs tem um valor grande. Corrigido na _Atualização cumulativa 8 para SQL Server 2012 SP1_, conforme descrito em KB [2923839](https://support.microsoft.com/kb/2923839).   
- O Change Data Capture para Oracle da Attunity para de funcionar quando as tabelas Oracle têm uma coluna com o tipo de dados Long. Corrigido na _Atualização cumulativa 2 para SQL Server 2012 SP3_ e _Atualização cumulativa 11 para SQL 2012 SP2_, conforme descrito em KB [3145983](https://support.microsoft.com/kb/3145983). 

## <a name="collect-detailed-logs"></a>Coletar logs detalhados 

Esta seção explica como coletar erros e eventos da instância da CDA. 

### <a name="management-console"></a>Console de gerenciamento

Você pode ver erros nas mensagens **Status** arquivadas no console de gerenciamento do Change Data Capture Designer para Oracle quando uma instância da CDA é realçada no painel esquerdo. 

### <a name="query-trace-table"></a>Consultar tabela de rastreamento

Você pode consultar a tabela de rastreamento no banco de dados da CDA dentro do SQL Server para ver os erros registrados. 

### <a name="save-output-from-basic-logging"></a>Salvar saída do log básico 

Para capturar o diagnóstico, selecione **Coletar Diagnósticos** na guia status do console de gerenciamento do Change Data Capture para Oracle. 

![Link Coletar Diagnósticos](media/known-issues-resolutions-with-cdc-for-oracle-attunity/collect-diagnostics.png)

Escolha uma hora de início e selecione um local para o arquivo de log. Em seguida, selecione **Criar** para iniciar a coleta de diagnósticos. 

![Link Coletar Diagnósticos](media/known-issues-resolutions-with-cdc-for-oracle-attunity/start-diagnostics.png)

### <a name="detailed-errors"></a>Erros detalhados

Você pode aumentar o nível de rastreamento coletado pela instância e repetir o cenário para coletar um log mais detalhado. Para fazer isso, selecione **Propriedades** em **Ações** e, em seguida, adicione uma nova propriedade na grade **Configurações Avançadas** na guia **Avançado**. Defina o nome da propriedade como `trace` e, em seguida, defina o valor como `SOURCE`. 

![Link Coletar Diagnósticos](media/known-issues-resolutions-with-cdc-for-oracle-attunity/properties.png)

Reproduza o erro e selecione a opção **Coletar Diagnósticos** para coletar logs. 

![Link Coletar Diagnósticos](media/known-issues-resolutions-with-cdc-for-oracle-attunity/collect-diagnostics.png)

## <a name="ora-00942-table-of-view-does-not-exist"></a>ORA-00942: a tabela da exibição não existe 

Esse é um erro comum, exibido no campo de mensagem de **Status** da instância da CDA. A instância tenta novamente várias vezes, portanto, o ícone de status mudará para verde momentaneamente, mas, em seguida, ele falhará com a exclamação vermelha e o status INESPERADO. 

![Erro do Oracle](media/known-issues-resolutions-with-cdc-for-oracle-attunity/oracle-error.png)

```
"ERROR","computername","ERROR","UNEXPECTED",
"ORACDC508E:Oracle method OCIStmtExecute failed with error: ORA-00942: table or view does not exist ","source","",""

"ERROR","computername","RUNNING","IDLE",
"ORACDC518E:Failed to verify archive log mode.","source","",""

"ERROR","computername","ERROR","UNEXPECTED",
"ORACDC517E:Oracle Call Interface (OCI) method failed: ORA-00942: table or view does not exist .","source","",""

"ERROR","computername","ERROR","UNEXPECTED",
"ORACDC414E:The Engine component failed with return code 1.","engine","",""
```

Isso acontece quando a conta do Oracle que está se conectando da instância da CDA ao servidor Oracle não tem permissão para ver exibições de log do sistema. 

### <a name="resolution"></a>Resolução

Para resolver esse erro, conceda ao usuário atualmente configurado as permissões apropriadas no sistema de banco de dados do Oracle ou altere qual conta está sendo usada para se conectar ao servidor Oracle da instância da CDA. 

A lista de todas as permissões necessárias é detalhada no arquivo de ajuda incluído na pasta `C:\Program Files\Change Data Capture for Oracle by Attunity\Attunity.SqlServer.XdbCdcDesigner.chm` de instalação, em Arquivos de Programas.  Consulte a página intitulada "Conectar-se a um banco de dados de origem Oracle" no arquivo .chm para obter a lista completa.

Você pode definir a conta de usuário selecionando o CDCInstance no painel esquerdo e selecionando o botão Propriedades no painel ações mais à direita na janela do **CDC Designer**. Você pode alterar a conta de autenticação de mineração de logs do Oracle na página de diálogo Propriedades.

![Erro do Oracle](media/known-issues-resolutions-with-cdc-for-oracle-attunity/oracle-connection.png)


  
## <a name="see-also"></a>Confira também  
 [Controle de alterações de dados &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [Trabalhar com dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)   
 [Administrar e monitorar a captura de dados de alteração &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
