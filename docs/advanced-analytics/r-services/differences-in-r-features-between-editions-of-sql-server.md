---
title: "Diferen&#231;as nos recursos de R entre edi&#231;&#245;es do SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "01/19/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Diferen&#231;as nos recursos de R entre edi&#231;&#245;es do SQL Server
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] está disponível nas seguintes edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   **Enterprise Edition**  
    
     Inclui ambos os serviços de R, para análise no banco de dados no SQL Server 2016, bem como o servidor de R (autônomo) no Windows, que pode ser usado para se conectar a uma variedade de bancos de dados e extrair dados para análise em grande escala, mas que não é executado no banco de dados. Também inclui **DeployR**, que pode ser usado para implantar modelos e scripts R como um serviço Web.  

     Sem restrições. Otimizar o desempenho e escalabilidade por meio de paralelização e streaming. Suopprts análise de grandes conjuntos de dados que não cabem na memória disponível, usando o **ScaleR** funções.  
  
     Análise de no banco de dados no SQL Server dá suporte a governança de recursos de scripts externos para personalizar o uso de recursos do servidor.  
  
-   **Developer Edition**  

    Mesmos recursos do Enterprise Edition; No entanto, a Developer Edition não pode ser usado em ambientes de produção.  

  
  
-   **Standard Edition**  
  
     Todos os recursos de análise no banco de dados está incluído com o Enterprise Edition, exceto para o controle de recursos flexíveis. Desempenho e escala também é limitado: os dados que podem ser processados deve caber na memória do servidor e o processamento é limitado a um thread de computação único, mesmo ao usar o **ScaleR** funções.
  
-   **Edições Express**  
  
     Somente edição Express com Advanced Services fornece serviços de R. As limitações de desempenho são semelhantes a Standard Edition.  
  
 Para obter mais informações sobre outros recursos do produto, consulte [recursos compatíveis com as edições do SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  

> [!NOTE]
>
> + Microsoft R Open é incluído em todas as edições.
> + O cliente do Microsoft R pode trabalhar com todas as edições.
  
## Enterprise Edition  
 Desempenho das soluções R [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser geralmente melhor do que qualquer implementação de R convencional, dado o mesmo hardware, como R pode ser executado usando recursos do servidor e, às vezes, distribuídos para vários processos usando o **ScaleR** funções.  
  
 Os usuários também podem esperar ver diferenças consideráveis em desempenho e escalabilidade para as mesmas funções de R Se executado no vs Enterprise Edition. Standard Edition. Motivos incluem suporte para processamento paralelo, streaming e maiores threads disponíveis para processamento de trabalho de R.  
  
 No entanto, o desempenho mesmo em hardware idêntico pode ser afetado por muitos fatores fora do código R, incluindo demandas concorrentes em recursos do servidor, o tipo de plano de consulta que é criado, alterações de esquema, a necessidade de atualizar estatísticas ou criar um novo plano de consulta, a fragmentação e muito mais. É possível que um procedimento armazenado contendo código de R pode ser executado em segundos em uma carga de trabalho, mas levar minutos quando há outros serviços em execução.  Portanto, é recomendável que você monitore vários aspectos do desempenho do servidor, inclusive redes para contextos de computação remota, quando quantificação de desempenho do trabalho de R.  

Também recomendamos que você configure [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) (disponível no Enterprise Edition) para personalizar a maneira que os trabalhos de R são priorizados ou manipulados em cargas de trabalho pesadas. Você pode definir funções de classificação para especificar a origem do trabalho R e priorizar determinadas cargas de trabalho, limitar a quantidade de memória usada pelas consultas SQL e controlar o número de processos paralelos usadas em uma base de carga de trabalho.  
  
## Developer Edition  
 Developer Edition fornece desempenho equivalente da Enterprise Edition; No entanto, o uso do Developer Edition não há suporte para ambientes de produção.  
  
  
## Standard Edition  
 Até mesmo Standard Edition devem oferecer algum benefício de desempenho, em comparação com pacotes de R padrão, dada a mesma configuração de hardware.  
  
 No entanto, Standard Edition não oferece suporte para o administrador de recursos. Usar o controle de recursos é a melhor maneira de personalizar os recursos do servidor para oferecer suporte a várias cargas de trabalho de R como modelo de treinamento e pontuação.  
  
 Standard Edition também fornece desempenho limitado e a escalabilidade em comparação com Enterprise e Developer Editions. Especificamente, todos os **ScaleR** funções e pacotes estão incluídos no Standard Edition, mas o serviço que inicia e gerencia scripts R é limitado o número de processos pode usar. Além disso, os dados processados pelo script devem caber na memória.  
  
  
## Express Edition com serviços avançados  
 Express Edition está sujeito às mesmas limitações do Standard Edition.  
  
## Consulte também  
 [Recursos com suporte nas edições do SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
  
  