---
title: "Log de mudanças para o SSDT (SQL Server Data Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b071f8b8-c8e5-44e0-bbb6-04804dd1863a
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8798c5319cdce7b68f71868722aacfbf4cb34d9f
ms.lasthandoff: 04/11/2017

---
# <a name="changelog-for-sql-server-data-tools-ssdt"></a>Log de mudanças para o SSDT (SQL Server Data Tools)
Este log de alterações é para o [SSDT (SQL Server Data Tools) para Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx), lançado junto com o [SQL Server 2016](https://msdn.microsoft.com/library/ms130214.aspx).  
  
Para postagens detalhadas sobre as novidades e alterações, visite o [Blog da equipe do SSDT](https://blogs.msdn.microsoft.com/ssdt/).  

## <a name="ssdt-165-for-sql-server-2016"></a>SSDT 16.5 (para SQL Server 2016)
Lançamento: 20 de outubro de 2016

Número de build: 14.0.61021.0

**Novidades**


### <a name="connection-improvements"></a>Aprimoramentos de conexão

* A nova caixa de pesquisa na guia **Procurar** ajuda a filtrar seus servidores locais, servidores de rede e bancos de dados do SQL do Azure. Isso é útil se você tem um grande número de servidores ou bancos de dados que aparecem nessas listas.
* A guia **Histórico** tem opções de menu de clique com o botão direito do mouse para fixar/desafixar favoritos e uma nova opção para remover conexões do histórico.

### <a name="sqlpackage-and-dacfx-api-improvements"></a>Aprimoramentos da API SqlPackage e DacFx

Agora, ao usar as APIs SqlPackage.exe e DacFx, você pode gerar um relatório de implantação, um script de implantação e publicar em um banco de dados, tudo de uma só vez. Isso economiza tempo para qualquer pessoa que gosta de guardar um relatório do que foi publicado durante a implantação. Outra vantagem é que, para cenários do Azure, são criados scripts separados para o banco de dados mestre e para o banco de dados de destino de implantação. Até agora era criado um único script que não era útil para implantações repetidas.

Para ações de Publicação e de Script do SqlPackage, foram adicionados dois novos argumentos.

* DeployScriptPath (nome curto: dsp). Esse é um caminho opcional no qual gravar o script de implantação. Para implantação do Azure, se houvesse comandos de TSQL para criar ou modificar o banco de dados, um script mestre seria gravado no mesmo caminho, mas com "Filename_Master.sql" como o nome de arquivo de saída.
* DeployReportPath (nome curto: drp). Esse é um caminho opcional no qual gravar o relatório de implantação.

Observe que para a ação de Script, os argumentos de caminho de saída existentes ou os novos argumentos específicos de script/relatório devem ser usados, mas não ambos.

Exemplo de uso:

**Ação de publicação**

```Sqlpackage.exe /a:Publish /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:”My\DeployScript.sql” /deployreportpath:”My\DeployReport.xml”```

**Ação de script**

```Sqlpackage.exe /a:Script /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:”My\DeployScript.sql” /deployreportpath:”My\DeployReport.xml”```

No DacFx, foram adicionadas duas novas APIs: DacServices.Publish() and DacServices.Script(). Elas também dão suporte à realização de ações de publicação + script + relatório em uma única operação. Exemplo de uso:

```
DacServices service = new DacServices(connectionString);
using(DacPackage package = DacPackage.Load(@"C:\My\db.dacpac")) {
var options = new PublishOptions() {
    GenerateDeploymentScript = true, // Should a deployment script be created?
    GenerateDeploymentReport = true, // Should an xml deploy report be created?
    DatabaseScriptPath = @"C:\My\OutputScript.sql", // optional path to save script to
    MasterDbScriptPath = @"C:\My\OutputScript_Master.sql", // optional path to save master script to
    DeployOptions = new DacDeployOptions()
};

// Call publish and receive deployment script & report in the results
PublishResult result = service.Publish(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);

// Call script and receive deployment script & report in results
result = service.Script(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);
```

**Analysis Services e Reporting Services**

O analisador DAX de designer tabular do SSAS teve o desempenho aprimorado ao trabalhar com grandes expressões DAX.
Para obter mais informações, leia a [Postagem de blog do Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/).

### <a name="fixed--improved-this-month"></a>Corrigido/aprimorado neste mês

**Ferramentas de banco de dados**

* [Bug de conexão 3055711](https://connect.microsoft.com/SQLServer/feedback/details/3055711/columns-cannot-be-selected-from-cross-apply-openjson-with-explicit-schema) – colunas não podem ser selecionadas de CROSS APPLY OPENJSON com esquema explícito
* Corrigido – problema com índices de tabela de histórico gerados automaticamente, em que o DacFx soltava índices na reimplantação
* Corrigido – problema com o analisador de lote DacFx que não analisava caracteres colchete ']' de escape, o que fazia com que a publicação falhasse
* Aprimorado – agora o SqlPackage inclui descrições para cada ação na saída da ajuda
* Corrigido – a opção "Lembrar senha", na caixa de diálogo de conexão, não era preservada ao editar opções avançadas e ao editar uma cadeia de conexão salva em Publicar, Comparação de Esquemas e outros arquivos
* Corrigido – para mostrar conexões na guia Histórico com IntegratedAuthentication = true, o campo de Autenticação, nas propriedades de conexão, foi deixado em branco. Agora é mostrado "Autenticação do Windows" conforme o esperado
* Corrigido – as alterações nas configurações do IntelliSense das Ferramentas do SQL Server em Ferramentas -> Opções -> Editor de Texto não eram preservadas
* Aprimorado – o botão Fixar/Desafixar na guia Histórico da caixa de diálogo de conexão, agora é mais compacto, reduzindo a probabilidade de aparecimento de uma barra de rolagem
* Corrigido – vários problemas de acessibilidade na caixa de diálogo conexão foram corrigidos.

**Analysis Services e Reporting Services**

* Foi corrigido um problema no designer de tabela SSDT AS em que, ao clicar na miniatura de barra de rolagem da grade de dados, gerava falha em determinadas situações
* Foi corrigido um problema em que a opção para representar a conexão como o usuário atual no designer de tabela SSDT AS não estava disponível
* Foi corrigido um problema no designer de tabela SSDT AS em que ao expandir a barra de fórmulas para muito longe poderia fazer com que o projeto se tornasse impossível de reabrir
* Foi corrigido uma falha no designer de tabela SSDT AS que ocorreria ao pressionar uma tecla, se a guia Tabela estivesse selecionada
* Foi corrigido um problema em projetos SSDT AS em que Analisar no Excel não se conectaria a versões de servidor AS de nível inferior

**Serviço de integração**

* Bug de conexão [1608896](https://connect.microsoft.com/SQLServer/feedback/details/1608896/move-multiple-integration-service-package-tasks) corrigido: mover vários pacotes de tarefas do serviço de integração





## <a name="ssdt-164-for-sql-server-2016"></a>SSDT 16.4 (para SQL Server 2016)
Lançamento: 20 de setembro de 2016

Número de build: 14.0.60918

**Novidades**

Agora há suporte para a Comparação de Esquemas nas APIs SqlPackage.exe e DacFx (Data-Tier Application Framework). Para obter detalhes, consulte [Comparação de Esquemas na SqlPackage e na Data-Tier Application Framework](https://blogs.msdn.microsoft.com/ssdt/2016/09/20/schema-compare-in-sqlpackage-and-the-data-tier-application-framework-dacfx/).

**Analysis Services – modo integrado de espaço de trabalho para SSDT Tabular (SSAS)**

O SSDT Tabular agora inclui uma instância do SSAS interna, que o SSDT Tabular inicia automaticamente em segundo plano se o modo de espaço de trabalho integrado estiver habilitado, para que você possa adicionar e exibir dados, tabelas e colunas no designer de modelo sem ter que fornecer uma instância de servidor de espaço de trabalho externo. Modo de espaço de trabalho integrado não será alterado quando SSDT Tabular trabalhar com um servidor de espaço de trabalho e o banco de dados. O que muda é onde o SSDT Tabular hospeda o banco de dados do espaço de trabalho. Para habilitar o modo de espaço de trabalho integrado, selecione a opção Espaço de Trabalho Integrado na caixa de diálogo Designer de Modelos de Tabela, exibida ao criar um novo projeto tabular. Para projetos tabulares existentes, que atualmente usam um servidor de espaço de trabalho explícito, você pode mudar para o modo de espaço de trabalho integrado, definindo o parâmetro Modo de Espaço de Trabalho Integrado como True na janela Propriedades, que é exibida quando você seleciona o arquivo Model.bim no Gerenciador de Soluções. Para obter detalhes, consulte a [Postagem de blog do Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/).

**Atualizações e correções**
**Ferramentas de banco de dados:**

- [Problema de conexão 3087775](https://connect.microsoft.com/SQLServer/feedback/details/3087775): tabelas temporais desfeitas em Ferramentas de Dados do VS, atualização 14.0.60629.0 de julho, "O valor não pode ser nulo. Nome do parâmetro: reportedElement "
- [Problema de conexão 1026648](https://connect.microsoft.com/SQLServer/feedback/details/1026648): IsPersistedNullable mostrado como diferente na comparação do SSDT
- [Problema de conexão 2054735](https://connect.microsoft.com/SQLServer/feedback/details/2054735): identidade é redefinida ao importar um BACPAC
- [Problema de conexão 2900167](https://connect.microsoft.com/SQLServer/feedback/details/2900167): a execução de testes de unidade do SSDT deixa arquivos temporários para trás
- [Problema de conexão 1807712](https://connect.microsoft.com/SQLServer/feedback/details/1807712): quebra de compatibilidade com versões anteriores – AppLocal e Nugetization

**Analysis Services e Reporting Services**

* Foi corrigido um problema no SSDT em que pop-ups de dicas de erros ficavam no meio do caminho ao editar colunas calculadas de DAX para DirectQuery.
* Foi corrigido um problema na grade tabular do SSDT AS em que o ícone do KPI não estava aparecendo na grade de medida quando o fator de dimensionamento do Windows era definido com alto DPI, acima de 200%.
* Foi corrigido um problema no SSDT AS em que colar dados de uma tabela grande poderia fazer com que o projeto tabular se tornasse sem resposta.
* Foi corrigido um problema no editor de modelo tabular do SSDT AS para marcar o modelo como necessário salvar as alterações, ao renomear o nome amigável da conexão.
* Foi corrigido um problema em projetos tabulares do SSDT AS em que a largura das colunas na caixa de diálogo Gerenciar Relações não podia ser redimensionada.
* Foi corrigido um problema nos modelos tabulares de nível de 1200 do SSDT AS em que colar dados do Excel com configurações de localidade, como alemão, não tratava corretamente a vírgula como um separador decimal.
* Foi corrigido um problema em projetos do SSDT AS com alguns conjuntos de ícones de KPI que poderiam produzir um erro "Não foi possível recuperar os dados para este visual".
* Foi corrigido um problema na caixa de diálogo de Propriedades do Projeto do SSDT AS para que seja corretamente ancorada ao ser redimensionada com o dimensionamento com alto DPI.
* Foi corrigido um problema em projetos do SSDT AS que pode ter causado um erro ao atualizar determinados modelos com tabelas coladas.
* Foi corrigido um problema no SSDT AS em que colar linhas de folha inteira do Excel era muito lento e criava muitas colunas indesejadas.
* Foi corrigido um problema no SSDT AS em que a análise e o realce de grandes expressões DataTable estáticas eram muito lentos ou parecia travar.
* Foi corrigido um problema no SSDT AS para adicionar medidas e valores de KPI à perspectiva atual selecionada no editor.
* Foi corrigido um problema no SSDT em que importar dados do SQL Azure para o projeto AS não dava suporte a tipos de esquema que não eram "dbo".



## <a name="ssdt-163-for-sql-server-2016"></a>SSDT 16.3 (para SQL Server 2016)
Lançamento: 15 de agosto de 2016

Número de build: 14.0.60812.0  

**Novidades**

- **Controle e numeração de versão:** as versões agora são rotuladas numericamente, em vez de por mês. Isso se alinha com a nova política do SSMS e simplifica os casos em que há várias versões ou hotfixes em um mês. Esta versão é a 16.3, que significa que é a terceira atualização após a versão RTM. Qualquer hotfix será 16.3.1 e assim por diante, com a nossa próxima atualização (planejada para o próximo mês) sendo a 16.4.
- **Analysis Services – Gerenciador de Modelos Tabular:** o Gerenciador de Modelos Tabular permite que você percorra convenientemente pelos diversos objetos de metadados em um modelo, como fontes de dados, tabelas, medidas e relações. Ele é implementado como uma janela de ferramentas separada que você pode exibir ao abrir o menu Exibir no Visual Studio, apontando para Outras Janelas e clicando em Gerenciador de Modelos Tabular. O Gerenciador de Modelos Tabular é exibido por padrão na área de Gerenciador de Soluções, em uma guia separada. O Gerenciador de Modelos Tabular organiza objetos de metadados em uma estrutura de árvore que se assemelha ao esquema de um modelo tabular de 1200 e tem muitos recursos novos.
- **Ferramentas de Banco de Dados – Always Encrypted**: esta versão oferece novas caixas de diálogo [Gerenciamento de Chaves Always Encrypted](https://msdn.microsoft.com/library/mt708953.aspx) para adicionar facilmente Chaves Mestras da Coluna ou Chaves de Criptografia da Coluna ao seu projeto de banco de dados ou a um banco de dados ao vivo no Pesquisador de Objetos do SQL Server. Esta versão dá suporte a certificados no Repositório de Certificados do Windows. Em versões futuras, o Azure Key Vault e os provedores CNG terão suporte.
    - Ao criar a Chave Mestra da Coluna ou a Chave de Criptografia da Coluna, você poderá notar que as alterações não estão refletidas no Pesquisador de Objetos do SQL Server, logo depois de clicar em Atualizar Banco de Dados. Para solucionar esse problema, atualize o nó do banco de dados no Pesquisador de Objetos do SQL Server.
    - Se você tentar criptografar uma coluna em uma tabela com os dados do Pesquisador de Objetos do SQL Server, poderá enfrentar uma falha. Este recurso tem suporte apenas em projetos de banco de dados do SSDT e SSMS. Suporte para SQL Server Object Explorer será habilitado em uma versão posterior.


**Atualizações e correções**
* **Ferramentas de banco de dados:**
    - **SSDT:**
        - Bug de conexão 1898001 [Foi corrigido um problema de descrição de coluna com limitação de 128 caracteres](https://connect.microsoft.com/SQLServer/feedback/details/1898001/column-description-limited-to-128-characters).
        - Foi corrigido um problema em que a publicação de um banco de dados do VS não aplicava a propriedade DatabaseServiceObjective no XML de perfil de publicação.
        - Bug de conexão 2900167 [Foi corrigido um problema de teste de unidade que deixava incorretamente arquivos temporários](http://connect.microsoft.com/SQLServer/feedback/details/2900167/running-ssdt-unit-tests-leaves-temp-files-behind).
        - Foi corrigido um problema em que a caixa de combinação Período de Retenção, em Configurações de Banco de Dados, ficava truncada.
        - Foi corrigido um problema de falta de verificação da senha antiga vazia nas propriedades do projeto CLR do SQL ao trocar de senha.
    - **DACFx:**
        - Foi corrigido um problema em que o nível de compatibilidade da DACFx não era atualizada para o erro SqlAzureV12.
        - Foi corrigido um problema em que propriedade IsAutoGeneratedHistoryTable era incorretamente excluída da comparação de modelos.

- **Analysis Services e Reporting Services**
    - **SSDT:**
        - Foi corrigido um problema no qual o modelo tabular não podia ser salvo quando a conexão do servidor era perdida.
        - Foi corrigido um problema no qual o SSDT se tornava sem resposta devido a um possível problema de loop infinito no AS.
        - Foi corrigido um problema de expressão DAX que causava comportamentos inconsistentes com base em como você confirmava a expressão.
        - Foi corrigido um problema de falha do VS ao criar KPIs.
        - Foi corrigido um problema que gerava relatórios inválidos para o SQL Server 2008 R2, 2012 e 2014.
        - Foi corrigido um problema de ordem de hierarquia que causava um erro de loop infinito para o projeto .dwpro.
        - Foi corrigido um problema do RDL RS em que fazer downgrade do RDL exigia uma recompilação completa, o que gerava confusão no usuário.
        - Foi corrigido um problema de KPI em que Ocultar das Ferramentas de Cliente não tinha nenhum efeito.
        

 
  
## <a name="ssdt-july-for-sql-server-2016"></a>SSDT julho (para SQL Server 2016)  
Lançamento: 30 de junho de 2016  
  
Número de build: 14.0.60629.0  
  
**Novidades**  
* **Suporte para Always Encrypted:** para bancos de dados que contêm colunas Always Encrypted, essa versão adiciona suporte completo para o Always Encrypted por meio de nossas principais APIs e da ferramenta de linha de comando (SqlPackage.exe). Você pode criar e publicar projetos de banco de dados com suporte total para todos os recursos Always Encrypted.  
* **Suporte aprimorado a Tabelas Temporais:** a experiência foi simplificada através da desvinculação de tabelas temporais antes das alterações e nova vinculação, depois que as alterações eram concluídas. Isso significa que as Tabelas Temporais têm paridade com outros tipos de tabela (padrão, na memória) em termos das operações as quais elas têm suporte. 
* **Alterações de instalação e da SqlPackage.exe:** alterações para isolar o SSDT do mecanismo do SQL Server e das atualizações do SSMS. Para obter detalhes, consulte [Alterações na instalação e nas atualizações do SSDT e da SqlPackage.exe](https://blogs.msdn.microsoft.com/ssdt/2016/06/30/changes-to-ssdt-and-sqlpackage-exe-installation-and-updates/).

 

**Atualizações e correções**
* **Ferramentas de banco de dados:**
    * De agora em diante o SSDT nunca desabilitará a TDE (Transparent Data Encryption) em um banco de dados. Anteriormente, uma vez que a opção de criptografia padrão nas configurações do banco de dados do projeto era desabilitada, a criptografia seria desligada. Com essa correção, a criptografia pode ser habilitada, mas nunca desabilitada durante a publicação. 
    * Aumento na contagem de novas tentativas e na resiliência para conexões de BD do SQL do Azure durante a conexão inicial.
    * Se o grupo de arquivos padrão não for PRIMARY, importar/publicar no Azure V12 falhará. Agora, essa configuração é ignorada durante a publicação.
    * Foi corrigido um problema em que ao exportar um banco de dados com um objeto com o Identificador entre Aspas ativado, a validação de exportação poderia falhar em alguns casos.
    * Foi corrigido um problema em que a opção TEXTIMAGE_ON era incorretamente adicionada para criações de tabela Hekaton, nas quais isso não é permitido.
    * Foi corrigido um problema em que a exportação de grande quantidade de dados demorava muito tempo, devido a uma gravação no arquivo model.xml depois da conclusão da fase de dados, o que fazia com que o conteúdo do arquivo .bacpac fosse regravado.
    * Foi corrigido um problema em que os usuários não apareciam na pasta Segurança para conexões de APS e SQL DW do Azure.


 * **Analysis Services e Reporting Services:**
    * Foi corrigido um problema de SxS com o provedor OLEDB do MSOLAP em que apenas o provedor de 32 bits era instalado, afetando o Excel 2016 de 64 bits ao se conectar ao SQL Server 2014 (foi não reproduzido com o instalações do ClickOnce do Office365, apenas em instalação do Excel de MSI).
    * Foi corrigido um problema de um caso incomum, para que fosse mais eficiente atualizar o modelo AS com tabelas coladas do nível de compatibilidade 1103 para o 1200, o que poderia resultar no erro "A relação usa uma ID de coluna inválida".
    * Foi corrigido um problema do SxS em que o SSDT-BI 2013, no mesmo computador, não podia mais importar dados em modelo AS após a desinstalação do SSDT 2015 (os cartuchos compartilhavam a configuração do Registro).
    * Robustez aprimorada para resolver problemas/falhas quando a conexão com o mecanismo AS era perdida (ou seja, o SSDT era deixado aberto durante a noite e o servidor AS reciclava ou outros casos em que a conexão era temporariamente perdida). 
    * Problemas corrigidos com caixas de diálogo abrindo em telas diferentes do VS em cenários de vários monitores. 
    * O suporte para colar de tabelas HTML (dados de grade) em tabelas coladas do modelo AS foi corrigido/habilitado. 
    * Foi corrigido o problema em que a atualização falhava ao atualizar uma tabela colada vazia no 1200 (usada somente como tabela de contêiner para medidas). 
    * Foi corrigido um problema com a atualização do modelo tabular AS com tabelas coladas no 1200 para solucionar um problema do mecanismo do AS com CalcTables (que são usadas para Tabelas Coladas no 1200), para realizar um processo completo em novas tabelas calc após a atualização. 
    * Foi corrigido um problema em que o cancelamento da criação de novos modelos de tabela calculada AS 1200 com a expressão DAX incompleta poderia falhar. 
    * Foi corrigido um problema ao importar o modelo 1200 do servidor AS no projeto SSDT AS, em que o nome do BD e um nome de tabela eram os mesmos. 
    * Foi corrigido um problema com a edição de medida do KPI no modelo tabular 1103. 
    * Foi corrigida uma referência de objeto que não definia a exceção encontrada ao colar uma medida de KPI na grade de um modelo 1200 do AS. 
    * Foi corrigido um problema em que uma coluna de uma tabela calculada não podia ser excluída da exibição de diagrama em modelos 1200. 
    * Foi corrigida uma referência de objeto que não definia exceção ao exibir as propriedades de arquivo de projeto model.bim enquanto estava na exibição de código. 
    * Foi corrigido um problema com a colagem de dados em uma grade de modelo AS para criar a tabela colada, que gerava valores incorretos em localidades internacionais, usando a vírgula como separador decimal. 
    * Foi corrigido um problema ao abrir o projeto do RS 2008 no SSDT e escolher não atualizá-lo. 
    * Problema corrigido na interface do usuário nas tabelas calculadas de modelos de nível de compatibilidade 1200 ao usar a formatação padrão para o tipo de coluna para permitir a alteração do tipo de formatação na interface do usuário. 
    

## <a name="ssdt-june-for-sql-server-2016"></a>SSDT Junho (para SQL Server 2016)  
Lançamento: 1 de junho de 2016  
  
Número de build: 14.0.60525.0 

A GA (Disponibilidade Geral) do SSDT foi lançada. A atualização GA do SSDT de junho de 2016 adiciona suporte para as atualizações mais recentes do SQL Server 2016 RTM e várias correções de bugs. Para obter detalhes, consulte [Atualização GA do SQL Server Data Tools de junho de 2016](https://blogs.msdn.microsoft.com/ssdt/2016/06/01/sql-server-data-tools-ga-update-for-june-2016/).

      

## <a name="ssdt-april-for-sql-server-2016-rc3"></a>SSDT Abril (para SQL Server 2016 RC3)  
Lançamento: 15 de abril de 2016  
  
Número de build: 14.0.60413.0  
  
**Banco de dados do SQL Server**  
* **Suporte para Always Encrypted:** para bancos de dados que contêm colunas Always Encrypted, o SSDT e o DacFx permite exibir e editar esses bancos de dados e publicar neles através de um projeto de banco de dados. Observe que o suporte para alterar colunas com a criptografia de coluna em vigor, será lançado em uma versão futura.  
* **Caixa de diálogo de Conexão e Pesquisador de Objetos do SQL Server:** várias correções e aprimoramentos.  
    * A página Detalhes, ao listar propriedades avançadas de conexão, foi revisada para mostrar a cadeia de conexão completa em uma caixa de várias linhas e para melhorar o suporte em computadores com alto DPI.  
    * Trouxemos de volta a caixa de diálogo de erro tradicional com erros de conexão detalhados. Isso ajuda, ao diagnosticar problemas de logon, com mensagens de erro mais claras e um rastreamento de pilha, para que os DBAs ou CSS possam obter as informações necessárias para ajudar a diagnosticar os problemas.  
    * Para usuários com permissões mínimas, corrigimos diversos problemas relacionados à listar bancos de dados na caixa de diálogo de Conexão e no Pesquisador de Objetos do SQL Server, exibindo a pasta Segurança e muito mais.  
    * O desempenho do banco de dados SQL do Azure, ao expandir o nó bancos de dados para listar todos os bancos de dados, foi aperfeiçoado.  
* **Instalador do SSDT:**  
    * Foi corrigido o problema em que o .NET era baixado durante ao desinstalar.  
    * O tamanho do instalador agora está definido corretamente em computadores com alto DPI.  
    * Foi removida a verificação de versão que bloqueava a instalação do SSDT se houvesse uma versão mais recente do SQL Server.  
    * Comparação de esquema: foi corrigido um problema de desempenho em que verificar/desmarcar vários itens levava muito tempo no Visual Studio.  
    * Suporte para o uso de LocalDB 2014 em computadores x86, já que não há versão x86 do SQL Server 2016.  
* **Build e implantação:**  
    * Foi corrigido o problema em que as colunas computadas não tinham suporte em Tabelas Temporais.  
    * A opção "Executar script de implantação no modo de usuário único" é ignorada na implantação no Azure V12, pois não há suporte para isso em cenários de nuvem.  
  
  
## <a name="ssdt-hotfix-for-sql-server-2016-rc2"></a>Hotfix SSDT (para SQL Server 2016 RC2)  
Lançamento: 5 de abril de 2016  
  
Número de build: 14.0.60329.0  
  
Esse build contém um hotfix para a versão do SSDT que fornece recursos para o SQL Server Integration Services. O build 14.0.60316.0 também pode ser usado com o Analysis Services e o Reporting Services no SQL Server 2016.   
  
Para obter esse hotfix, use os [links para download nesta postagem de blog](https://blogs.msdn.microsoft.com/ssdt/2016/04/05/ssdt-preview-update-rc2/).  
  
Desenvolvedores de relatórios, se você cria novos relatórios usando este build do SSDT, [leia os problemas conhecidos e as soluções alternativas](https://blogs.msdn.microsoft.com/ssdt/2016/04/05/ssdt-preview-update-rc2/) para um problema temporário nos relatórios do SSRS, encontrados somente nesse hotfix.  
  
## <a name="ssdt-hotfix-for-sql-server-2016-rc0"></a>Hotfix SSDT (para SQL Server 2016 RC0)  
Lançamento: 18 de março de 2016  
  
Número de build: 14.0.60316.0  
  
Esse build contém um hotfix para a versão do SSDT que fornece recursos para o SQL Server 2016 RC0. Não há nenhuma versão RC1 do SSDT neste momento. O build 14.0.60316.0 pode ser usado com a RC0 ou RC1 do SQL Server 2016.  
      
## <a name="ssdt-february-2016-preview-for-sql-server-2016-rc0"></a>Visualização do SSDT de fevereiro de 2016 (para SQL Server 2016 RC0)  
Lançamento: 7 de março de 2016  
  
Número de build: 14.0.60305.0  
  
-   **Modelos de projeto do SQL Server**  
  
    Nenhum anúncio para esta versão de visualização do SSDT. Consulte [Novidades no Mecanismo de Banco de Dados](https://msdn.microsoft.com/library/bb510411.aspx) para saber mais sobre outros recursos neste lançamento.  
  
-   **Modelos de projeto de pacote do SSIS**  
  
    O Designer do SSIS cria e mantém pacotes para o SQL Server 2016, 2014 ou 2012. Novos modelos renomeados como partes. O conector para Hadoop do SSIS oferece suporte ao formato ORC. Consulte [Novidades do Integration Services](https://msdn.microsoft.com/library/bb522534.aspx) para obter detalhes.  
  
-   **Modelos de projeto do SSAS (projetos de modelo Tabular)**  
  
    A atualização deste mês do Analysis Services oferece suporte às pastas de exibição para modelos Tabulares e há suporte em pacotes do SSIS para todos os modelos criados com o novo nível de compatibilidade do SQL Server 2016. Para obter mais informações. consulte [Novidades no Analysis Services (postagem de blog)](http://blogs.msdn.com/b/analysisservices/archive/2016/01/28/what-s-new-for-sql-server-2016-analysis-services-in-ctp3-3.aspx) para obter detalhes.  
  
-   **Modelos de projeto de relatório do SSRS**  
  
    Nenhum anúncio para esta versão de visualização do SSDT. Consulte [Novidades no Reporting Services](https://msdn.microsoft.com/library/ms170438.aspx) para saber mais sobre outros recursos neste lançamento.  
  
## <a name="ssdt-january-2016-preview"></a>Visualização do SSDT de janeiro de 2016  
Lançamento: 4 de fevereiro de 2016  
  
Número de build: 14.0.60203.0  
  
-   **Modelos de projeto do SQL Server**  
  
    Nenhum anúncio para esta versão de visualização do SSDT. Consulte [Novidades no Mecanismo de Banco de Dados](https://msdn.microsoft.com/library/bb510411.aspx) para saber mais sobre outros recursos neste CTP.  
  
-   **Modelos de projeto de pacote do SSIS**  
  
    Adiciona suporte para componentes de origem e de destino do ODBC, uma tarefa de controle CDC,  
      um componente de origem e de separador de CDC, um Microsoft Connector para SAP BW e um Integration Services Feature Pack para o Azure. Consulte [Novidades do Integration Services](https://msdn.microsoft.com/library/bb522534.aspx) para obter detalhes.  
  
-   **Modelos de projeto do SSAS**  
  
    Inclui melhorias para modelos tabulares no nível de compatibilidade 1200, colunas calculadas e segurança no nível de linha para modelos no modo DirectQuery, conversões de metadados de modelo, execução do script TMSL na Tarefa Executar DDL do Analysis Services do SSIS e muitas correções de bugs.  
    Consulte [Novidades no Analysis Services (MSDN)](https://msdn.microsoft.com/library/bb522628.aspx) ou [Novidades no Analysis Services (postagem de blog)](http://blogs.msdn.com/b/analysisservices/archive/2016/01/28/what-s-new-for-sql-server-2016-analysis-services-in-ctp3-3.aspx) para obter detalhes.  
  
-   **Modelos de projeto de relatório do SSRS**  
  
    Nenhum anúncio para esta versão de visualização do SSDT. Consulte [Novidades no Reporting Services](https://msdn.microsoft.com/library/ms170438.aspx) para saber mais sobre outros recursos neste CTP.  
  
## <a name="ssdt-december-2015-preview"></a>Visualização do SSDT de dezembro de 2015  
  
-   Os **Modelos de projeto do SQL Server** incluem correções de bug para a caixa de diálogo Conexão, listas de histórico recentes, uso adequado do contexto de autenticação definido na propriedade de conexão ao carregar uma lista de banco de dados.  
  
    -   Valor de tempo limite da conexão de teste alterado para 15 segundos.  
  
    -   Crie uma regra de firewall de servidor do Banco de Dados SQL do Microsoft Azure se o IP do cliente não estiver registrado ao carregar uma lista de banco de dados.  
  
    -   Suporte à programação de recursos do SQL Server 2016 CTP 3.2.  
  
-   Os **modelos de projeto do SSAS** adicionam suporte para a criação de tabelas calculadas com base em expressões DAX e outros objetos já definidos no modelo.  
  
-   As adições do **modelo de projeto de pacote SSIS** incluem suporte ao conector Hadoop do SSIS para o formato de arquivo do Avro e a autenticação Kerberos.   
    Observe que o suporte de designer do SSIS para SSIS 2012 e 2014 ainda não está incluído nesta atualização.  
  
## <a name="ssdt-november-2015-preview"></a>Visualização do SSDT de novembro de 2015  
  
-   **Modelos de projeto do SQL Server**. Visualização da experiência aprimorada de conexão do SQL Server e do Banco de Dados SQL do Microsoft Azure.  
  
-   **Modelos de projeto de pacote SSIS**. Melhoria no desempenho do catálogo de SSIS: o desempenho da maioria das exibições de catálogo do SSIS para o usuário que não é administrador do SSIS foi aprimorado.  
  
-   Os **modelos de projeto do SSAS** incluem melhorias para projetos de modelo Tabular no Analysis Services. Você pode usar o comando **Exibir Código** para exibir a definição de modelo em JSON. Se não estiver usando uma edição completa do Visual Studio 2015, você precisará dela para obter o editor de JSON. Você pode baixar o [Visual Studio Community Edition](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) gratuitamente.  
  
## <a name="ssdt-october-2015-preview"></a>Visualização do SSDT de outubro de 2015  
  
-   Novos modelos de projeto para BI (modelos do Analysis Services, relatórios do Reporting Services e pacotes do Integration Services). Todos os modelos de projeto do SQL Server agora estão em um único SSDT.  
  
-   Novos recursos do SSIS, incluindo o conector para Hadoop e o modelo de fluxo de controle. Além disso, o tamanho máximo do buffer da tarefa de fluxo de dados foi flexibilizado.  
  
-   Suporte de recursos do SQL Server 2016 CTP 3.0 para projetos de banco de dados relacional.  
  
-   Várias correções de bugs no SSIS e suporte para o sistema operacional Windows 7.  
  
## <a name="ssdt-september-2015-preview"></a>Visualização do SSDT de setembro de 2015  
  
-   O suporte a vários idiomas é uma novidade nesta visualização.  
  
## <a name="ssdt-august-2015-preview"></a>Visualização do SSDT de agosto de 2015  
  
-   Novo programa Setup.exe autônomo para instalar o SSDT.  Você não precisa usar uma versão modificada da instalação do SQL Server. Esta versão do SSDT inclui um modelo de projeto para a criação de bancos de dados relacionais implantados no SQL Server ou no Banco de Dados SQL do Microsoft Azure.  
  
## <a name="see-also"></a>Consulte também  
[Baixar o SQL Server Data Tools &#40;SSDT&#41;](../ssdt/download-sql-server-data-tools-ssdt.md)  
[Versões anteriores do SQL Server Data Tools &#40;SSDT e SSDT-BI&#41;](../ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md)  
[Novidades do Mecanismo de Banco de Dados](https://msdn.microsoft.com/library/bb510411.aspx)  
[Novidades do Analysis Services](https://msdn.microsoft.com/library/bb522628.aspx)  
[Novidades do Integration Services](https://msdn.microsoft.com/library/bb522534.aspx)  
  

