---
title: "Diferenças nos recursos de aprendizado de máquina entre as edições do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b9b520b7fc7e97498f4b46a43ad991558025123a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---

# <a name="differences-in-machine-learning-features-between-editions-of-sql-server"></a>Diferenças nos recursos de aprendizado de máquina entre as edições do SQL Server
 
 Suporte para o aprendizado de máquina está disponível nas seguintes edições do SQL Server 2016 e 2017 do SQL Server:

## <a name="summary-of-differences"></a>Resumo das diferenças

-   **Enterprise Edition**
    
     SQL Server 2017 inclui serviços de aprendizado de máquina (em bancos de dados. SQL Server 2016 inclui serviços de R. Esse recurso oferece suporte à análise no banco de dados no SQL Server, incluindo o uso do SQL Server como um contexto de computação.
     
     SQL Server 2017 inclui aprendizado de máquina do Microsoft Server (autônomo). SQL Server 2016 inclui o Microsoft R Server (autônomo). Esse recurso oferece suporte a operacionalização do que não requer o uso do SQL Server como um contexto de computação de aprendizado de máquina.

     Não existem restrições sobre esses recursos no Enterprise Edition, que fornece a otimizar o desempenho e escalabilidade por meio de paralelização e streaming. Essa edição também maximiza o uso de suporte de plataforma para execução paralela e streaming.
     
     Análise no banco de dados usando o SQL Server oferece suporte à administração de recursos de scripts externos para personalizar o uso de recursos do servidor.
     
     Edições mais recentes do Microsoft R Server incluem uma versão aprimorada do mecanismo operacionalização que dá suporte à implantação rápida e segura e compartilhar soluções de R. Para obter mais informações, consulte [mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package).

-   **Developer Edition**

     Mesmos recursos que a Enterprise Edition. No entanto, a Developer Edition não pode ser usada em ambientes de produção.  
  
-   **Standard Edition**

     Todos os recursos de análise no banco de dados está incluído com o Enterprise Edition, com exceção de governança de recursos. Desempenho e escala também está limitado: os dados que podem ser processados devem se ajustar na memória do servidor, e o processamento é limitado a um thread único de computação, mesmo ao usar o **RevoScaleR** funções.
  
-   **Express e Web edições**
  
     Somente Express Edition com Advanced Services inclui a recursos de aprendizado de máquina. As limitações de desempenho são semelhantes à Standard Edition. Não se destina a edição Web para tarefas como criar modelos de aprendizado de máquina. No entanto, você pode usar a função de previsão para executar pontuação usando modelos treinados em outro lugar.

-   **Banco de Dados SQL do Azure**
  
     Recursos de aprendizado de máquina, como R e script de Python atualmente não têm suporte no banco de dados do SQL Azure.
     
     Para obter mais informações e anúncios sobre quando este recurso estará disponível, consulte o blog do SQL Server: [Python no SQL Server 2017: aprimorada de aprendizado de máquina no banco de dados](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)


### <a name="languages-supported-in-all-editions"></a>Idiomas com suporte em todas as edições

Os idiomas de aprendizado de máquina a seguir têm suporte para todas as edições:

+ SQL Server 2017: R e Python
+ SQL Server 2016: Somente para R

O Microsoft R Open é incluído em todas as edições.

O Microsoft R Client pode trabalhar com todas as edições.

## <a name="machine-learning-in-enterprise-edition"></a>Enterprise Edition de aprendizado de máquina

Desempenho das soluções de aprendizado de máquina em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espera geralmente superam implementações usando R convencional, dado o mesmo hardware. Que é porque, no SQL Server, as soluções de R podem ser executadas usando recursos do servidor e, às vezes, são distribuídas para vários processos usando o **RevoScaleR** funções. 

Desempenho não foi avaliado para soluções de Python, como o recurso ainda está em desenvolvimento, mas alguns dos mesmos benefícios podem ser aplicados.

Os usuários também podem esperar ver diferenças consideráveis no desempenho e escalabilidade para o mesmo computador, solução de aprendizado se executar no vs Enterprise Edition. Standard Edition. Motivos incluem suporte para paralela maiores threads disponíveis para aprendizado de máquina, processamento e streaming (ou agrupamento), que permite que as funções de RevoScaleR lidar com mais dados do que pode caber na memória. 

No entanto, o desempenho mesmo em hardware idêntico pode ser afetado por vários fatores fora do código R ou Python. Esses fatores incluem concorrentes demandas de recursos do servidor, o tipo de plano de consulta que é criado, as alterações de esquema, a necessidade de atualizar estatísticas ou criar um novo plano de consulta, fragmentação e muito mais. É possível que um procedimento armazenado contendo código R ou Python pode ser executado em segundos em uma carga de trabalho, mas levar minutos, se houver outros serviços em execução.  Portanto, é recomendável que você monitore vários aspectos de desempenho do servidor, incluindo a rede para contextos de computação remota, ao avaliar o desempenho de aprendizado de máquina.

Também é recomendável que você configure [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) (disponível na edição Enterprise) para personalizar a maneira que os trabalhos de script externo são priorizados ou tratados sob cargas de trabalho excessiva no servidor. Você pode definir funções de classificação para especificar a origem do trabalho de script externo e priorizar determinadas cargas de trabalho, para limitar a quantidade de memória usada pelas consultas SQL e controlar o número de processos paralelos usados em uma base de carga de trabalho.

## <a name="machine-learning-in-developer-edition"></a>Edição de desenvolvedor de aprendizado de máquina

A Developer Edition fornece desempenho equivalente à Enterprise Edition, no entanto, não há suporte para o uso da Developer Edition em ambientes de produção.

## <a name="machine-learning-in-standard-edition"></a>Standard Edition de aprendizado de máquina

Até mesmo a Standard Edition deverá oferecer algum benefício de desempenho, em comparação com pacotes de R padrão, considerando a mesma configuração de hardware.

Edição Standard não oferece suporte para o administrador de recursos. Usar o controle de recursos é a melhor maneira de personalizar os recursos do servidor para dar suporte a várias cargas de trabalho como modelo de treinamento e pontuação.

A Standard Edition também oferece desempenho e escalabilidade limitados em comparação com a Enterprise e a Developer Edition. Todos os **RevoScaleR** funções e pacotes são incluídos com a Standard Edition, mas o serviço que inicia e gerencia os scripts de R é limitado no número de processos, ele pode usar. Além disso, os dados processados pelo script devem caber na memória.  As mesmas restrições se aplicam às soluções que usam **revoscalepy**.

## <a name="machine-learning-in-express-edition-with-advanced-services"></a>Express Edition com serviços avançados de aprendizado de máquina

A Express Edition está sujeita às mesmas limitações da Standard Edition.

## <a name="machine-learning-in-web-edition"></a>Web Edition de aprendizado de máquina

Edição Web não oferece suporte à execução de scripts de R ou Python. No entanto, você pode usar a função de previsão para executar [pontuação nativo](../sql-native-scoring.md) em um modelo que foi treinado em uma instância diferente do SQL Server ou do servidor de R e, em seguida, salvo no formato binário necessário.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, consulte:

+ [Edições e componentes do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [Edições e componentes do SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)

Para obter mais informações sobre outros recursos do SQL Server, consulte:

+ [Edições e recursos com suporte para SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md) 

Para obter mais informações sobre como você pode otimizar sua solução para grandes conjuntos de dados e os recursos do Microsoft R, consulte o [Microsoft R Server](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips) documentação.
