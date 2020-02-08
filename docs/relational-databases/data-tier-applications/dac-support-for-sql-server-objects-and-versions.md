---
title: Suporte de DAC para objetos e versões do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- data-tier application [SQL Server], supported objects
- objects [SQL Server], data-tier applications
ms.assetid: b1b78ded-16c0-4d69-8657-ec57925e68fd
author: stevestein
ms.author: sstein
ms.openlocfilehash: c0e0f85e21898ccf61d7c205305fc9179edc2af4
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68810580"
---
# <a name="dac-support-for-sql-server-objects-and-versions"></a>Suporte de DAC para objetos e versões do SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Um aplicativo da camada de dados (DAC) dá suporte aos objetos do [!INCLUDE[ssDE](../../includes/ssde-md.md)] mais usados.  
  
 **Neste tópico**  


> [!IMPORTANT]
> Este artigo é válido para o SQL Server 2012, mas não para o SQL Server 2014 ou posterior.
> Para ver artigos do DAC sobre o SQL 2012 e versões anteriores, consulte os links a seguir:
> 
> - https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ee240739(v=sql.105)
> - https://docs.microsoft.com/previous-versions/sql/sql-server-2012/hh753459(v=sql.110)


-   [Objetos SQL Server com suporte](#SupportedObjects)  
  
-   [Suporte a aplicativo da camada de dados das versões do SQL Server](#SupportByVersion)  
  
-   [Limitações de implantação de dados](#DeploymentLimitations)  
  
-   [Considerações adicionais para ações de implantação](#Considerations)  
  
##  <a name="SupportedObjects"></a> Objetos SQL Server com suporte  
 Somente objetos com suporte podem ser especificados em um aplicativo da camada de dados enquanto ele é criado ou editado. Você não pode extrair, registrar ou importar um DAC de um banco de dados existente que contenha objetos sem suporte em um DAC. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferece suporte aos objetos a seguir em um DAC.  
  
|||  
|-|-|  
|DATABASE ROLE|FUNCTION: Com valor de tabela embutida|  
|FUNCTION: Com valor de tabela de várias instruções|FUNCTION: Escalar|  
|INDEX: Clusterizado|INDEX: Não clusterizado|  
|INDEX: Espacial|INDEX: Exclusivo|  
|LOGIN|Permissões|  
|Associações de função|SCHEMA|  
|Estatísticas|STORED PROCEDURE: Transact-SQL|  
|Sinônimos|TABLE: Restrição CHECK|  
|TABLE: Collation|TABLE: Coluna, incluindo colunas computadas|  
|TABLE: Restrição, Padrão|TABLE: Restrição, Chave Estrangeira|  
|TABLE: Restrição, Índice|TABLE: Restrição, Chave Primária|  
|TABLE: Restrição, Exclusiva|TRIGGER: DML|  
|TYPE: HIERARCHYID, GEOMETRY, GEOGRAPHY|TYPE: Tipo de Dados definido pelo usuário|  
|TYPE: Tipo de Tabela definido pelo usuário|USER|  
|VIEW||  
  
##  <a name="SupportByVersion"></a> Suporte a aplicativo da camada de dados das versões do SQL Server  
 As versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm níveis diferentes de suporte para operações do DAC. Todas as operações do DAC com suporte de uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm suporte de todas as edições dessa versão.  
  
 As instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] oferecem suporte às seguintes operações DAC:  
  
-   Exportar e extrair têm suporte em todas as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Todas as operações têm suporte no [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] e em todas as versões do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]e do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].  
  
-   Todas as operações têm suporte no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Service Pack 2 (SP2) ou posterior e no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 ou posterior.  
  
 O DAC Framework inclui as ferramentas do lado do cliente por compilar e processar pacotes do DAC e arquivos de exportação. Os produtos a seguir incluem o DAC Framework  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] incluem o DAC Framework 3.0, com suporte a todas as operações de DAC.  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 e o Visual Studio 2010 SP1 incluíam o DAC Framework 1.1, que oferece suporte a todas as operações de DAC, exceto a exportação e a importação.  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o Visual Studio 2010 incluíam o DAC Framework 1.0, que é compatível com todas as operações de DAC, menos exportação, importação e atualização no local.  
  
-   As ferramentas de cliente de versões anteriores de SQL Server ou Visual Studio não oferecem suporte a operações de DAC.  
  
 Um pacote de DAC ou arquivo de exportação criados com uma versão do DAC Framework não podem ser processados por uma versão anterior do DAC Framework. Por exemplo, um pacote do DAC extraído usando as ferramentas de cliente [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] que usa as ferramentas de cliente [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] não pode ser implantado.  
  
 Um pacote de DAC ou arquivo de exportação criados com uma versão do DAC Framework podem ser processados por uma versão posterior do DAC Framework. Por exemplo, um pacote de DAC extraído usando as ferramentas de cliente do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] podem ser implantadas usando as ferramentas de cliente [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 ou superiores.  
  
##  <a name="DeploymentLimitations"></a> Limitações de implantação de dados  
 Observe estas limitações de fidelidade do mecanismo de implantação de dados da Estrutura DAC no SQL Server 2012 SP1. As limitações se aplicam às seguintes ações da Estrutura DAC: implantar ou publicar um arquivo .dacpac, e importar um arquivo .bacpac.  
  
1.  A perda de metadados em certas condições e tipos de base nas colunas sql_variant. Nos casos afetados, você verá um aviso com a seguinte mensagem:  **Algumas propriedades em alguns tipos de dados usados dentro de uma coluna sql_variant não são preservadas quando a implantação é feita pela Estrutura DAC.**  
  
    -   Tipos base MONEY, SMALLMONEY, NUMERIC, DECIMAL:  A precisão não é preservada.  
  
        -   Tipos de base DECIMAL/NUMERIC com precisão 38: os metadados de sql_variant “TotalBytes” são sempre definidos como 21.  
  
    -   Todos os tipos de base de texto:  A ordenação padrão de banco de dados é aplicada a todo o texto.  
  
    -   Tipos de base BINARY:  A propriedade de comprimento máximo não é preservada.  
  
    -   Tipos de base TIME, DATETIMEOFFSET:  A precisão é sempre definida como 7.  
  
2.  Perda de dados nas colunas sql_variant. No caso afetado, você verá um aviso com a seguinte mensagem:  **Haverá perda de dados quando um valor em uma coluna sql_variant DATETIME2 com escala maior que 3 for implantado pela estrutura DAC. O valor DATETIME2 está limitado a uma escala igual a 3 durante a implantação.**  
  
    -   Tipo de base DATETIME2 com escala maior que 3: a escala é limitada ao valor igual a 3.  
  
3.  Ocorre falha na operação de implantação com as condições em colunas sql_variant a seguir. Nos casos afetados, você verá uma caixa de diálogo com a seguinte mensagem:  **Falha na operação devido a limitações de dados na Estrutura DAC.**  
  
    -   Tipos base DATETIME2, SMALLDATETIME e DATE:  Se o valor estiver fora do intervalo de data e hora, por exemplo, o ano será anterior a 1753.  
  
    -   Tipo de base DECIMAL, NUMERIC: quando a precisão do valor é maior que 28.  
  
##  <a name="Considerations"></a> Considerações adicionais para ações de implantação  
 Observe as seguintes considerações para ações da implantação de dados da Estrutura DAC:  
  
-   **Extrair/Exportar** – Nas ações que usam a Estrutura DAC para criar um pacote de um banco de dados – por exemplo, extrair um arquivo .dacpac, exportar um arquivo .bacpac – essas restrições não se aplicam. Os dados no pacote são uma representação de fidelidade total dos dados no banco de dados de origem. Se alguma dessas condições estiver presente no pacote, o log de extração/exportação conterá um resumo dos problemas através das mensagens observadas anteriormente. Esse é um aviso ao usuário sobre problemas potenciais de implantação de dados com o pacote criado. O usuário também verá a seguinte mensagem de resumo no log:  **Essas limitações não afetam a fidelidade dos tipos de dados e valores armazenados no pacote DAC que tenha sido criado pela Estrutura DAC; elas se aplicam apenas aos tipos de dados e valores resultantes da implantação de um pacote DAC em um banco de dados. Para obter mais informações sobre os dados afetados e como solucionar essa limitação, confira**[este tópico](https://go.microsoft.com/fwlink/?LinkId=267086).  
  
-   **Implantar/Publicar/Importar** – Nas ações que usam a Estrutura DAC para implantar um pacote em um banco de dados, como implantar ou publicar um arquivo .dacpac, e importar um arquivo .bacpac, essas limitações se aplicam. Os dados que resultam no banco de dados de destino não podem conter uma representação de fidelidade total dos dados no pacote. O log Implantar/Importar conterá uma mensagem, observada acima, para cada instância em que o problema for encontrado. A operação será bloqueada por erros (consulte a categoria 3 anterior), mas continuará com os outros avisos.  
  
     Para obter mais informações sobre os dados que são afetados neste cenário e como solucionar essa limitação para ações de implantação/publicação/importação, confira [este tópico](https://go.microsoft.com/fwlink/?LinkId=267087).  
  
-   **Soluções alternativas** – as operações de extração e de exportação gravarão arquivos de dados BCP de fidelidade total nos arquivos .dacpac ou .bacpac. Para evitar limitações, use o utilitário de linha de comando BCP.exe do SQL Server para implantar dados de fidelidade total em um banco de dados de destino de um pacote de DAC.  
  
## <a name="see-also"></a>Consulte Também  
 [Aplicativos da camada de dados](../../relational-databases/data-tier-applications/data-tier-applications.md)  
  
  
