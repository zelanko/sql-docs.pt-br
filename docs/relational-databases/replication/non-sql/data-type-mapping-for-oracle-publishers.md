---
title: "Mapeamento de tipo de dados para Publicadores Oracle  | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "publicação Oracle [replicação do SQL Server], mapeamento de tipos de dados"
  - "publicação Oracle [replicação do SQL Server], publicação Oracle"
  - "mapeando tipos de dados [replicação do SQL Server]"
ms.assetid: 6da0e4f4-f252-4b7e-ba60-d2e912aa278e
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# Mapeamento de tipo de dados para Publicadores Oracle 
  Tipos de dados Oracle e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de dados nem sempre correspondem exatamente. Onde possível, o tipo de dados correspondente é selecionado automaticamente ao publicar uma tabela de Oracle. Em casos em que o mapeamento de um único tipo de dados não é claro, mapeamentos alternativos de tipo de dados são fornecidos. Para obter informações sobre como selecionar mapeamentos alternativos, consulte "Especificando Mapeamentos Alternativos de Tipos de Dados”, mais adiante neste tópico.  
  
 A tabela a seguir mostra como os tipos de dados são mapeados por padrão entre o Oracle e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando os dados são movidos de um Publicador Oracle para o Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . A coluna de Alternativas indica se mapeamentos alternativos estão disponíveis.  
  
|Tipo de dados de Oracle|Tipo de dados do SQL Server|Alternativas|  
|----------------------|--------------------------|------------------|  
|BFILE|VARBINARY(MAX)|Sim|  
|BLOB|VARBINARY(MAX)|Sim|  
|CHAR([1-2000])|CHAR([1-2000])|Sim|  
|CLOB|VARCHAR(MAX)|Sim|  
|DATE|DATETIME|Sim|  
|FLOAT|FLOAT|Não|  
|FLOAT([1-53])|FLOAT([1-53])|Não|  
|FLOAT([54-126])|FLOAT|Não|  
|INT|NUMERIC(38)|Sim|  
|INTERVAL|DATETIME|Sim|  
|LONG|VARCHAR(MAX)|Sim|  
|LONG RAW|IMAGE|Sim|  
|NCHAR([1-1000])|NCHAR([1-1000])|Não|  
|NCLOB|NVARCHAR(MAX)|Sim|  
|NUMBER|FLOAT|Sim|  
|NUMBER([1-38])|NUMERIC([1-38])|Não|  
|NUMBER([0-38],[1-38])|NUMERIC([0-38],[1-38])|Sim|  
|NVARCHAR2 ([1-2000])|NVARCHAR([1-2000])|Não|  
|RAW ([1-2000])|VARBINARY([1-2000])|Não|  
|REAL|FLOAT|Não|  
|ROWID|CHAR(18)|Não|  
|TIMESTAMP|DATETIME|Sim|  
|TIMESTAMP(0-7)|DATETIME|Sim|  
|TIMESTAMP(8-9)|DATETIME|Sim|  
|TIMESTAMP(0-7) WITH TIME ZONE|VARCHAR(37)|Sim|  
|TIMESTAMP(8-9) WITH TIME ZONE|VARCHAR(37)|Não|  
|TIMESTAMP(0-7) WITH LOCAL TIME ZONE|VARCHAR(37)|Sim|  
|TIMESTAMP(8-9) WITH LOCAL TIME ZONE|VARCHAR(37)|Não|  
|UROWID|CHAR(18)|Não|  
|VARCHAR2([1-4000])|VARCHAR([1-4000])|Sim|  
  
## Considerações para o mapeamento do tipo de dados  
 Pense nos seguintes problemas de tipo de dados ao replicar dados de um banco de dados de Oracle.  
  
### Tipos de dados sem-suporte  
 Os seguintes tipos de dados não têm suporte; não podem ser replicadas as colunas que têm estes tipos:  
  
-   Tipos de objeto  
  
-   Tipos XML  
  
-   Varrays  
  
-   Tabelas aninhadas  
  
-   Colunas que usam REF  
  
### O tipo de dados de DATE.  
 Datas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] variam de 1753 D.C. a 9999 d.C. enquanto as datas no Oracle vão de 4712 a.C. a 4712 d.C. Se uma coluna do tipo DATE contém valores que estão fora do intervalo do SQL Server, selecione um tipo de dados alternativo para a coluna, que é VARCHAR(19).  
  
### Tipos FLOAT e NUMBER  
 A escala e precisão especificadas durante o mapeamento de tipos de dados FLOAT e NUMBER dependem da escala e precisão especificadas para a coluna usando o tipo de dados no banco de dados do Oracle. A precisão é o número de dígitos em um número. A escala é o número de dígitos à direita da casa decimal em um número. Por exemplo, o número 123,45 tem uma precisão de 5 e uma escala de 2.  
  
 O Oracle permite números a serem definidos com a escala maior que a precisão, tal como NUMBER(4,5), mas o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requer que a precisão seja igual ou maior que a escala. Para garantir que não há truncamento de dados, se a escala for maior que a precisão no Publicador Oracle, a precisão é definida igual à escala quando o tipo de dados for mapeado: NUMBER (4,5) ele seria mapeado como NUMERIC (5,5).  
  
> [!NOTE]  
>  Se você não especificar a escala e a precisão para NUMBER, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa o padrão máximo de escala (8) e precisão (38). É recomendável que você defina uma escala e precisão específicas no Oracle para melhor armazenamento e desempenho quando os dados forem replicados.  
  
### Tipos de objeto grande  
 O Oracle suporta até 4 gigabytes (GB), enquanto que o SQL Server suporta até 2 GB. Dados replicados acima de 2 GB são truncados.  
  
 Se uma tabela de Oracle incluir uma coluna de BFILE, os dados para a coluna serão armazenados no sistema de arquivos. A conta de usuário administrativo da replicação deve dispor de acesso ao diretório no qual os dados estão armazenados, usando a seguinte sintaxe:  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 Para obter mais informações sobre tipos de objetos grandes, consulte a seção "Considerações para objetos grandes" em [Considerações de Design e limitações para Publicadores Oracle](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
## Especificando mapeamentos alternativos de tipo de dados  
 Tipicamente, o padrão de mapeamento de tipo de dados é apropriado, porém para muitos tipos de dados do Oracle, você pode selecionar um mapeamento de tipo de dados a partir de um conjunto de mapeamentos alternativos, ao invés de usar o padrão. Há dois modos para especificar os mapeamentos alternativos:  
  
-   Substitua o padrão em uma base por artigo usando procedimentos armazenados ou o Assistente para Nova Publicação.  
  
-   Globalmente altere o padrão para todos os artigos futuros usando procedimentos armazenados (não são alterados os padrões para os artigos existentes).  
  
 Para especificar mapeamentos alternativos de tipo de dados, consulte [Specify Data Type Mappings for an Oracle Publisher](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md).  
  
## Consulte também  
 [Configurar um publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Considerações de design e limitações para Publicadores Oracle](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)   
 [Visão geral da Publicação Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  