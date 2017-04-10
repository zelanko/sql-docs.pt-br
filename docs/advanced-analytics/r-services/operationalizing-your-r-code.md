---
title: "Operacionaliza&#231;&#227;o do C&#243;digo R | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f15696b1-2479-4e5f-ac5e-4beaf958a043
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Operacionaliza&#231;&#227;o do C&#243;digo R
  Os desenvolvedores de banco de dados são responsáveis por integrar várias tecnologias e reunir os resultados para que possam ser compartilhados por toda a empresa. O desenvolvedor de banco de dados trabalha com os desenvolvedores de aplicativos, os desenvolvedores de SQL e os cientistas de dados para criar soluções, recomendar métodos de gerenciamento de dados e projetar e implantar soluções. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] fornece muitos benefícios aos desenvolvedores que trabalham com os cientistas de dados.  
  
-   **Interagir com scripts de R usando [!INCLUDE[tsql](../../includes/tsql-md.md)].** Os desenvolvedores de banco de dados e aplicativos, bem como os analistas que criam relatórios, podem invocar um script R chamando-a partir de um procedimento armazenado do sistema.  
  
     Para obter mais informações sobre a sintaxe básica, consulte [sp_execute_external_script & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e [usando o código R em T-SQL](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md).  
 
    Para um exemplo de como colocar em operação R código usando procedimentos armazenados, consulte [no banco de dados de análise para desenvolvedores do SQL](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md).
  
     A integração com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também significa que você pode executar scripts R usando o [!INCLUDE[tsql](../../includes/tsql-md.md)] e incorporar os resultados em seu aplicativo. Por exemplo, você pode criar um relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que executa um script R e, em seguida, exibe os gráficos juntamente com as previsões no relatório.  
  
-   **Desempenho e escalabilidade.** Embora a linguagem de código-fonte aberto R têm limitações, o pacote RevoScaleR APIs fornecidas pelo [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] pode operar em grandes conjuntos de dados e se beneficiar de vários segmentos, com vários núcleos, vários processos computações no banco de dados.  
  
     Se sua solução R usa agregações complexas ou envolve grandes conjuntos de dados, você pode aproveitar as agregações de memória e os índices columnstore altamente eficientes do SQL, deixando o código R tratar do processamento dos cálculos estatísticos e das pontuações.  
  
-   **Ferramentas de desenvolvimento e gerenciamento padrão.** Não é necessária qualquer ferramenta adicional para administração ou implantação; todos os trabalhos de R podem ser chamados por meio da invocação de um procedimento armazenado.  
  
     Além disso, o mesmo código R executado nos dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser facilmente usado em outras fontes de dados, como o Hadoop.  
  
 Esta seção descreve os conceitos que você precisa entender para converter soluções R com êxito e implantá-las na produção usando o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
## Nesta seção

[Trabalhando com tipos de dados R](../../advanced-analytics/r-services/working-with-r-data-types.md)

[Convertendo código R para uso em serviços de R](../../advanced-analytics/r-services/converting-r-code-for-use-in-r-services.md)

##  <a name="bkmk_RelatedTasks"></a> Tarefas relacionadas  
  
[Ajuste de desempenho para SQL Server R serviços](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
## Consulte também  
 [Recursos e tarefas do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)   
 [sp_execute_external_script & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  
  