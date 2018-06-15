---
title: Tutoriais do SQL Server Python | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c99e5605dad537fddef20fbd091a61cc4e711471
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31201938"
---
# <a name="sql-server-python-tutorials"></a>Tutoriais do SQL Server Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece uma lista de tutoriais e exemplos que demonstram o uso de Python com 2017 do SQL Server. Por meio desses exemplos e demonstrações, você aprenderá:

+ Como executar o Python do T-SQL
+ Quais são os contextos de computação local e remoto e como você pode executar o código Python usando o computador do SQL Server
+ Como encapsular o código Python em um procedimento armazenado
+ Otimizando o código Python para um ambiente de produção do SQL
+ Cenários do mundo real para incorporar o aprendizado de máquina em aplicativos

Para obter informações sobre os requisitos e a instalação, consulte [pré-requisitos](#bkmk_Prerequisites).

## <a name="bkmk_pythontutorials"></a>Tutoriais do Python

+ [Python em execução no T-SQL](run-python-using-t-sql.md)

   Conheça os fundamentos de como chamar Python em T-SQL, usando o mecanismo de extensibilidade pioneira no SQL Server 2016.

+ [Criar uma modelo no Python usando revoscalepy de aprendizado de máquina](use-python-revoscalepy-to-create-model.md)

   Esta lição demonstra como você pode executar código de um terminal Python remoto, usando o contexto de computação do SQL Server. Você deve ser um pouco familiarizado com as ferramentas Python e ambientes. Código de exemplo é fornecido que cria um modelo usando **rxLinMod**, da nova **revoscalepy** biblioteca. 

+ [Análise de Python no banco de dados para desenvolvedores em SQL](sqldev-in-database-python-for-sql-developers.md)

    Este passo a passo de ponta a ponta demonstra o processo de criação de uma solução completa de Python usando procedimentos armazenados T-SQL. Todo o código Python é incluído.


## <a name="python-samples"></a>Exemplos de Python

Esses exemplos e demonstrações fornecidas pela equipe de desenvolvimento do SQL Server realce maneiras que você pode usar a análise incorporada em aplicativos do mundo real.

+ [Criar um modelo de previsão usando Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  Saiba como uma empresa de aluguel ski pode usar o aprendizado de máquina para prever locações futuras, que ajuda a equipe e plano de negócios para atender às demandas futuras.

  > [!TIP]
  > Agora inclui nativo de pontuação de modelos de Python!

+ [Executar o cliente clustering usando Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Saiba como usar o algoritmo Kmeans para executar o cluster sem supervisão de clientes.

## <a name="bkmk_Prerequisites"></a>Pré-requisitos

Para usar esses tutoriais, você deve ter o SQL Server 2017, e você deve instalar explicitamente e, em seguida, habilitar o recurso, serviços de aprendizado de máquina (no banco de dados). 

2017 do SQL Server dá suporte a idiomas de R e Python, mas não está instalado ou habilitado por padrão. A execução do Python requer que a estrutura de extensibilidade ser habilitada e que você selecione Python como o idioma a instalar. 

### <a name="post-installation-configuration-tips"></a>Dicas de configuração de pós-instalação

Depois de executar a instalação do SQL Server, talvez você precise executar algumas etapas adicionais para garantir que o Python e o SQL Server estão se comunicando:

+ Habilitar o recurso de execução do script externo executando `sp_configure 'external scripts enabled', 1`.
+ Reinicie o servidor. 
+ Abra o **serviços** painel para verificar se a barra inicial foi iniciado. 
+ Verifique se o serviço que chama o tempo de execução externo tem as permissões necessárias. Para obter mais informações, consulte [habilitar a autenticação implícita](../r/add-sqlrusergroup-to-database.md).
+ Abrir uma porta no firewall para SQL Server e habilite os protocolos de rede necessários.
+ Certifique-se de que o logon do SQL ou a conta de usuário do Windows tem as permissões necessárias para se conectar ao servidor, a leitura de dados e para criar os objetos de banco de dados necessários para o exemplo.

Consulte este artigo para alguns problemas comuns: [Solucionando problemas de serviços de aprendizado de máquina](../machine-learning-troubleshooting-faq.md)

### <a name="resource-management"></a>Gerenciamento de recursos

Você pode instalar o R e Python no mesmo computador, mas executar ambos pode exigir recursos consideráveis. Se você obtiver erros de "memória insuficiente", ou se a execução de trabalhos de aprendizado de máquina é que a entidade de segurança se destina ao uso do servidor, você pode reduzir a quantidade de memória alocada para o mecanismo de banco de dados. Para obter mais informações, consulte [Gerenciando e monitorando Python no SQL Server](../python/managing-and-monitoring-python-solutions.md).

## <a name="see-also"></a>Consulte também

[Tutoriais de R para SQL Server](sql-server-r-tutorials.md)
