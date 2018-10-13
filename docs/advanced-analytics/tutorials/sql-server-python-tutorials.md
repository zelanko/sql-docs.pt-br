---
title: Tutoriais do Python do SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 541675c22ddbe347f67119d8cba82f75955382e6
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48877980"
---
# <a name="sql-server-python-tutorials"></a>Tutoriais do Python do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece uma lista de tutoriais e exemplos que demonstram o uso do Python com o SQL Server 2017. Por meio desses exemplos e demonstrações, você aprenderá:

+ Como executar o Python no T-SQL
+ Quais são os contextos de computação local e remoto e como você pode executar o código do Python usando o computador do SQL Server
+ Como encapsular o código do Python em um procedimento armazenado
+ Otimizando o código do Python para um ambiente de produção do SQL
+ Cenários do mundo real para a inserção de aprendizado de máquina em aplicativos

Para obter informações sobre os requisitos e instalação, consulte [pré-requisitos](#bkmk_Prerequisites).

## <a name="bkmk_pythontutorials"></a>Tutoriais do Python

+ [Execução de Python no T-SQL](run-python-using-t-sql.md)

   Conheça os fundamentos de como chamar o Python no T-SQL, usando o mecanismo de extensibilidade pioneiro no SQL Server 2016.

+ [Criar um modelo de machine learning no Python usando revoscalepy](use-python-revoscalepy-to-create-model.md)

   Esta lição demonstra como você pode executar o código de um terminal de Python remoto, usando o contexto de computação do SQL Server. Você deve ser um pouco familiarizado com os ambientes e ferramentas do Python. Código de exemplo é fornecido que cria um modelo usando **rxLinMod**, da nova **revoscalepy** biblioteca. 

+ [Análise de Python no banco de dados para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md)

    Este passo a passo de ponta a ponta demonstra o processo de criação de uma solução completa do Python usando procedimentos armazenados T-SQL. Todo o código Python é incluído.


## <a name="python-samples"></a>Exemplos de Python

Esses exemplos e demonstrações fornecidas pela equipe de desenvolvimento do SQL Server realçam maneiras que você pode usar a análise inserida em aplicativos do mundo real.

+ [Criar um modelo preditivo usando o Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  Saiba como uma empresa de aluguel de Esqui pode usar o aprendizado de máquina para prever o futuras locações, que ajuda a equipe e plano de negócios para atender às demandas futuras.

  > [!TIP]
  > Agora inclui a pontuação nativa de modelos em Python!

+ [Executar o cliente clustering usando o Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Saiba como usar o algoritmo Kmeans para executar o clustering sem supervisão de clientes.

## <a name="bkmk_Prerequisites"></a>Pré-requisitos

Para usar esses tutoriais, você deve ter o SQL Server 2017 e você deve instalar explicitamente e, em seguida, habilitar o recurso, serviços de Machine Learning (no banco de dados). 

SQL Server 2017 dá suporte a linguagens Python e R, mas não está instalado ou habilitado por padrão. Execução de Python requer que a estrutura de extensibilidade esteja habilitada e que você selecione Python como o idioma a instalar. 

### <a name="post-installation-configuration-tips"></a>Dicas de configuração de pós-instalação

Depois de executar a instalação do SQL Server, talvez você precise executar algumas etapas adicionais para garantir que o Python e o SQL Server estão se comunicando:

+ Habilitar o recurso de execução do script externo executando `sp_configure 'external scripts enabled', 1`.
+ Reinicie o servidor. 
+ Abra o **Services** painel para verificar se o Launchpad foi iniciado. 
+ Certifique-se de que o serviço que chama o tempo de execução externo tem as permissões necessárias. Para obter mais informações, consulte [habilitar a autenticação implícita](../security/add-sqlrusergroup-to-database.md).
+ Abrir uma porta no firewall para SQL Server e habilite os protocolos de rede necessários.
+ Certifique-se de que o logon do SQL ou a conta de usuário do Windows tem as permissões necessárias para se conectar ao servidor, para ler dados e crie quaisquer objetos de banco de dados exigidos pelo exemplo.

Consulte este artigo para alguns problemas comuns: [de solução de problemas dos serviços do Machine Learning](../machine-learning-troubleshooting-faq.md)

### <a name="resource-management"></a>Gerenciamento de recursos

Você pode instalar o R e Python no mesmo computador, mas executar ambos pode exigir recursos substanciais. Se você obtiver erros de "memória insuficiente", ou se a execução de trabalhos de aprendizado de máquina é que a entidade de segurança se destina ao uso do servidor, você pode reduzir a quantidade de memória é alocada ao mecanismo de banco de dados. Para obter mais informações, consulte [Gerenciando e monitorando o Python no SQL Server](../python/managing-and-monitoring-python-solutions.md).

## <a name="see-also"></a>Confira também

[Tutoriais de R para SQL Server](sql-server-r-tutorials.md)
