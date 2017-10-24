---
title: Interoperabilidade de Python | Microsoft Docs
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32762183ff5273998848978238788cc830319b91
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="python-interoperability"></a>Interoperabilidade de Python

Este tópico descreve os componentes do Python que são instalados quando você habilitar o recurso **serviços de aprendizado de máquina (no banco de dados)** e selecione Python como o idioma.

> [!NOTE]
> Suporte para Python é um recurso de pré-lançamento e ainda está em desenvolvimento.

## <a name="python-components"></a>Componentes do Python

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]Não modifique os executáveis de Python. O tempo de execução do Python é instalado, independentemente das ferramentas do SQL e é executado fora do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] processo.

A distribuição que está associada um determinado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instância pode ser encontrada na pasta associada à instância.

Por exemplo, se você instalou os serviços de aprendizado de máquina com a opção de Python na instância padrão, procure em:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER`

Instalação de serviços de aprendizado de máquina do SQL Server 2017 adiciona a distribuição Anaconda de Python. Especificamente, os instaladores Anaconda 3 são usados, com base na ramificação Anaconda 4.3. O nível esperado do Python para o SQL Server 2017 é Python 3.5.

## <a name="new-in-this-release"></a>Novo nesta versão

Para obter uma lista de pacotes com suporte para a distribuição da Anaconda, consulte o site de análise de continuidade: [a lista de pacotes Anaconda](https://docs.continuum.io/anaconda/pkg-docs)

Serviços de aprendizado de máquina no SQL Server 2017 também inclui o novo **revoscalepy** biblioteca do Python.

Essa biblioteca fornece funcionalidade equivalente para que o **RevoScaleR** pacote para o Microsoft R. Em outras palavras, ele oferece suporte à criação de contextos de computação remota, bem como um vários modelos de aprendizado de máquina escalonável, tais como **rxLinMod**. Para obter mais informações sobre RevoScaleR, consulte [distribuída e a computação paralela com ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).

Porque o suporte a Python é um recurso de pré-lançamento e ainda está em desenvolvimento, o **revoscalepy** biblioteca atualmente inclui apenas um subconjunto da funcionalidade RevoScaleR. 

Adições futuras podem incluir o [Microsoft cognitivas Toolkit](https://www.microsoft.com/research/product/cognitive-toolkit/). Essa biblioteca anteriormente conhecido como CNTK, oferece suporte a uma variedade de modelos de rede neural, incluindo redes convolutional (CNN), redes recorrentes (RNN) e redes de longa memória termo curto (LSTM).

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

[Bibliotecas de Python e tipos de dados](python-libraries-and-data-types.md)

