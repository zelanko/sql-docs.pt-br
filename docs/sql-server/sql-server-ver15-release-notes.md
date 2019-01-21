---
title: Notas sobre a versão do SQL Server 2019 | Microsoft Docs
ms.date: 12/07/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 9d810c1a76eb4253c6d11abce7cd9992260c3708
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2019
ms.locfileid: "54298943"
---
# <a name="sql-server-2019-preview-release-notes"></a>Notas sobre a versão a versão prévia do SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  > [!div class="nextstepaction"]
  > [Compartilhe seus comentários sobre o Sumário do SQL Docs!](https://aka.ms/sqldocsurvey)

Este artigo descreve as limitações e os problemas conhecidos para as versões do [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP (Community Technology Preview). Para obter informações relacionadas, consulte:
- [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)

> [!NOTE]
> Versões prévias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] são disponibilizadas para você experimentar os recursos da versão futura. Elas não são compatíveis nem licenciadas para uso em produção. Os cenários a seguir não são explicitamente compatíveis:
>
> - Instalação lado a lado com outras versões do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
> - Atualizar uma instância existente do SQL Server de qualquer versão

**Experimente[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]!**
- [![Baixar do Centro de Avaliação](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=862101) [Baixe o [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] para instalação no Windows](https://go.microsoft.com/fwlink/?LinkID=862101)
- Instalar no Linux para [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md), [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) e [Ubuntu](../linux/quickstart-install-connect-ubuntu.md).
- [Executar no SQL Server 2019 no Docker](../linux/quickstart-install-connect-docker.md).

## <a name="ctp-22-december-2018"></a>CTP 2.2 (dezembro de 2018)
[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] O CTP 2.2 é a última versão pública do [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] O CTP 2.2 está disponível apenas como Evaluation Edition. Nenhuma outra edição está disponível. O suporte para o CTP 2.2 é descrito em `license_Eval.rtf` com a mídia de instalação.

Suporte limitado pode ser encontrado em um dos seguintes locais:

- Fóruns
  - [Comentários do SQL Server](https://aka.ms/sqlfeedback)
  - [Introdução ao SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqlgetstarted)
  - [Transact-SQL](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=transactsql)
  - [SQL Server, documentação](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqldocumentation)

- Ou envie um tweet para [@SQLServer](https://twitter.com/SQLServer) com [#sqlhelp](https://twitter.com/search?q=%23sqlhelp)

### <a name="documentation-ctp-22"></a>Documentação (CTP 2.2)

- **Problema e impacto sobre o cliente**: A documentação para o SQL Server 2019 (15.x) é limitada e o conteúdo está incluído no conjunto de documentação [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O conteúdo nesses artigos específico para o SQL Server 2019 (15.x) será indicado com **Aplica-se a**.

- **Problema e impacto para o cliente**: a documentação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode ser filtrada por versão. Use o controle na parte superior esquerda de cada página de documentação para filtrar os requisitos. 

- **Problema e impacto sobre o cliente**: Nenhum conteúdo offline está disponível para o SQL Server 2019 (15.x).

### <a name="hardware-and-software-requirements"></a>Requisitos de hardware e software

- **Problema e impacto sobre o cliente**: Os requisitos de hardware e software ainda estão sendo analisados e não são definitivos para a versão do produto.

  - **Hardware**
    - [Windows – requisitos de processador, memória e sistema operacional](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux – requisitos do sistema](../linux/sql-server-linux-setup.md#system)
  - **Software**
    - Windows Server 2016 ou posterior. Para ver os requisitos adicionais, consulte [Requisitos para instalação do SQL Server](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - Microsoft .NET Framework 4.6.2. Disponível no [Centro de Download](https://www.microsoft.com/download/details.aspx?id=53344).
    - Para Linux, consulte [Linux – plataformas compatíveis](../linux/sql-server-linux-setup.md#supportedplatforms)

### <a name="updated-compiler"></a>Compilador atualizado

- **Problema e impacto sobre o cliente**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] é compilado com um compilador atualizado. O CTP 2.1 tinha um problema conhecido em que os resultados de ponto flutuante e outros cenários de conversão podem ter retornado um valor diferente de versões anteriores por causa do compilador atualizado. CTP 2.2 inclui trabalho para garantir que os cenários afetados retornem os mesmos resultados que as versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Da versão CTP 2.2 em diante, desconhecemos quaisquer problemas restantes. Relate quaisquer anomalias de resultado em comparação com [!INCLUDE[ss2017](../includes/sssqlv14-md.md)] à equipe do [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]](http://aka.ms/sqlfeedback) imediatamente.

- **Solução alternativa**: N/A

- **Aplica-se ao**: SQL Server 2019 CTP 2.2, CTP 2.1

### <a name="sql-server-integration-services-ssis-page-deployment-after-switching-db-to-single-user-mode-and-then-switching-back"></a>Implantação de página do SSIS (SQL Server Integration Services) depois de mudar o banco de dados para o modo de usuário único e, em seguida, mudar de volta

- **Problema e impacto sobre o cliente**: Depois que o SSISDB muda do modo de usuário único para o modo de multiusuário, o seguinte erro pode ser relatado ao ser implantado um pacote:

  `Cannot continue the execution because the session is in the kill state.`

- **Solução alternativa**: Pare e reinicie a instância do SQL Server e mude o SSISDB de volta para o modo de multiusuário.

- **Aplica-se ao**: SQL Server 2019 versão prévia CTP 2.2, CTP 2.1

### <a name="utf-8-collations"></a>Agrupamentos UTF-8

- **Problema e impacto sobre o cliente**: Os agrupamentos UTF-8 habilitados não poderão ser usados com alguns dos outros recursos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O UTF-8 não é compatível quando os recursos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a seguir são usados:

  - Servidor vinculado
  - OLTP in-memory
  - Tabela externa para PolyBase

  > [!Note]
  > No momento, não há nenhuma interface do usuário compatível para escolher os agrupamentos UTF-8 habilitados no Azure Data Studio ou SSDT (SQL Server Data Tools). A versão mais recente do SSMS ([!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]) é compatível com a seleção de agrupamentos UTF-8 habilitados na interface do usuário.
 
- **Solução alternativa**: Não há solução alternativa para CTPs do [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].

- **Aplica-se ao**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.2, CTP 2.1, CTP 2.0.

### <a name="sql-graph"></a>SQL Graph

- **Problema e impacto sobre o cliente**: Ferramentas que dependem de DacFx, como importação-exportação, não funcionarão para os novos recursos de grafo – DML de restrições ou mesclagem do Microsoft Edge. Os scripts em [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] podem não funcionar.

- **Solução alternativa**: Escrever scripts [!INCLUDE[tsql](../includes/tsql-md.md)] e execute-os no servidor usando [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou SQLCMD funcionará. A exportação ou a importação de objetos de banco de dados que criam restrições do Microsoft Edge, têm nova sintaxe de DML de mesclagem ou criam exibições/tabelas derivadas em objetos de grafo não funcionarão. Os usuários precisarão criar manualmente esses objetos no seu banco de dados usando scripts [!INCLUDE[tsql](../includes/tsql-md.md)]. 

- **Aplica-se ao**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.2, CTP 2.1, 2.0.

### <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted com enclaves seguros

- **Problema e impacto sobre o cliente**: Os cálculos avançados estão aguardando várias otimizações de desempenho, incluindo a funcionalidade limitada (sem indexação etc.) e estão desabilitados por padrão no momento.

- **Solução alternativa**: Para habilitar cálculos avançados, execute `DBCC traceon(127,-1)`. Para obter detalhes, consulte [Habilitar cálculos avançados](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave).

- **Aplica-se ao**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.2, CTP 2.1, 2.0.

## <a name="ctp-21-october-2018"></a>CTP 2.1 (outubro de 2018)

O [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1 é a versão pública anterior do [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].

### <a name="udf-inlining"></a>Inlining do UDF

- **Problema e impacto sobre o cliente**: Existem cenários específicos em que chamadas aninhadas a funções definidas pelo usuário embutidas não validam corretamente a segurança.
  
- **Solução alternativa**: Desabilite o inlining do UDF para tais UDFs usando a configuração `INLINE = OFF`.

- **Aplica-se ao**: SQL Server 2019 CTP 2.1

### <a name="sql-server-integration-service---fuzzy-lookup-transformation"></a>SQL Server Integration Service ‒ Transformação Pesquisa Difusa

- **Problema/impacto sobre o cliente**: A Transformação Pesquisa Difusa falhará com o seguinte erro se for definida para reutilizar o índice:

  `The specified delimiters do not match the delimiters used to build the pre-existing match index "...". This error occurs when the delimiters used to tokenize fields do not match. This can have unknown effects on the matching behavior or results.`

- **Solução alternativa**: N/A

- **Mais informações**: N/A  

- **Aplica-se a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1

### <a name="lightweight-query-profiling-infrastructure"></a>Infraestrutura de criação de perfil de consulta leve

- **Problema e impacto sobre o cliente**: Executar o comando `ALTER DATABASE SCOPED CONFIGURATION SET LIGHTWEIGHT_QUERY_PROFILING = ON` retorna um erro de sintaxe. Todos os cenários que dependem da execução desse comando falharão.

  > [!NOTE]
  > Atualmente, a LWP (infraestrutura de criação de perfil de consulta leve) não pode ser controlada no nível de banco de dados individuais e permanece habilitada para todos os bancos de dados por padrão. Para obter mais informações sobre LWP, confira [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

- **Solução alternativa**: Não há solução alternativa para CTPs do [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].

- **Aplica-se ao**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1 e CTP 2.0.

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
