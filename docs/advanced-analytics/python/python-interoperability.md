---
title: Interoperabilidade do Python com o SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 11/03/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 3477c941d81f860996776cf89bfc3ffe7dbc81af
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="python-interoperability-with-sql-server"></a>Interoperabilidade do Python com o SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve os componentes do Python que são instalados quando você habilitar o recurso **serviços de aprendizado de máquina (no banco de dados)** e selecione Python como o idioma.

## <a name="python-components"></a>Componentes do Python

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Não modifique os executáveis de Python. O tempo de execução do Python é instalado, independentemente das ferramentas do SQL e é executado fora do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] processo.

A distribuição que está associada um determinado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instância pode ser encontrada na pasta associada à instância.

Por exemplo, se você instalou os serviços de aprendizado de máquina com a opção de Python na instância padrão, procure em:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

Instalação de serviços de aprendizado de máquina do SQL Server 2017 adiciona a distribuição Anaconda de Python. Especificamente, os instaladores Anaconda 3 são usados, com base na ramificação Anaconda 4.3. O nível esperado do Python para o SQL Server 2017 é Python 3.5.

## <a name="new-python-packages-in-this-release"></a>Novos pacotes do Python nesta versão

Para obter uma lista de pacotes com suporte para a distribuição da Anaconda, consulte o site de análise de continuidade: [a lista de pacotes Anaconda](https://docs.continuum.io/anaconda/pkg-docs)

Serviços de aprendizado de máquina no SQL Server 2017 também inclui o novo **revoscalepy** biblioteca do Python.

Essa biblioteca fornece funcionalidade equivalente para que o **RevoScaleR** pacote para o Microsoft R. Em outras palavras, ele oferece suporte à criação de contextos de computação remota, bem como um vários modelos de aprendizado de máquina escalonável, tais como **rxLinMod**. Para obter mais informações sobre RevoScaleR, consulte [distribuída e a computação paralela com ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).

O [microsoftml para Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) pacote é instalado como parte do aprendizado de máquina do SQL Server quando você adiciona o Python para sua instalação. Este pacote contém muitos algoritmos aprendizado de máquina que foram otimizados para velocidade e a precisão, bem como transformações para trabalhar com texto e imagens de linha. Para obter detalhes, consulte [usando o pacote de MicrosoftML com o SQL Server](https://docs.microsoft.com/sql/advanced-analytics/using-the-microsoftml-package).

Microsoftml e revoscalepy estão estritamente ligadas; fontes de dados usadas em microsoftml são definidos como objetos revoscalepy. Limitações de contexto na transferência de revoscalepy para microsoftml de computação. Ou seja, toda a funcionalidade está disponível para operações de locais, mas a mudança para um contexto de computação remota exige RxInSqlServer.

## <a name="using-python-in-sql-server"></a>Usando Python no SQL Server

Importar o **revoscalepy** módulo em seu código Python e, em seguida, chamar funções do módulo, como outras funções de Python.

Dados de entrada de Python devem ser tabulares. Todos os resultados de Python devem ser retornados na forma de um **pandas** quadro de dados.

Você pode executar o código Python em T-SQL, incorporando o script em um procedimento armazenado.

Ou, execute o código de um IDE Python local e ter o script executado no computador do SQL Server, definindo um contexto de computação remota.

Você pode trabalhar com dados locais, obter dados do SQL Server ou outras fontes de dados ODBC ou usar o formato de arquivo XDF para trocar dados com outras fontes, ou com soluções de R.

**Para obter mais informações**

+ Funções com suporte: [novidades revoscalepy](what-is-revoscalepy.md) 
+ Suporte para tipos de dados do Python: [bibliotecas Python e tipos de dados](python-libraries-and-data-types.md)
+ Suporte para fontes de dados: ODBC bancos de dados, SQL Server e os arquivos XDF
+ Suporte para contextos de computação: local ou do SQL Server

### <a name="licensing"></a>Licenciamento

Como parte da instalação dos serviços de aprendizado de máquina com Python, você deve concordar com os termos da licença pública GNU.

## <a name="see-also"></a>Consulte também

[Bibliotecas Python e tipos de dados](python-libraries-and-data-types.md)
