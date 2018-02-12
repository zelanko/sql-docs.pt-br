---
title: Tutoriais do SQL Server Python | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 09/19/2017
vapplies_to:
- SQL Server 2017
dev_langs:
- Python
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 42a9339f5983eeef28250db7a384f37efd4dad9d
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
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

   Você criará um modelo usando **rxLinMod**, da nova **revoscalepy** biblioteca. Você vai lançar o código de um terminal Python remoto, mas a modelagem serão executadas no contexto de computação do SQL Server.

+ [Análise de Python no banco de dados para desenvolvedores em SQL](sqldev-in-database-python-for-sql-developers.md)

  NOVO! Crie uma solução completa de Python usando procedimentos armazenados T-SQL. Todo o código Python é incluído.

+ [Implantar e consumir um modelo de Python](..\python\publish-consume-python-code.md)

  Saiba como implantar um modelo de Python usando a versão mais recente do Microsoft Server de aprendizado de máquina.

## <a name="python-samples"></a>Exemplos de Python

Esses exemplos e demonstrações fornecidas pela equipe de desenvolvimento do SQL Server realce maneiras que você pode usar a análise incorporada em aplicativos do mundo real.

+ [Criar um modelo de previsão usando Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  Saiba como uma empresa de aluguel ski pode usar o aprendizado de máquina para prever locações futuras, que ajuda a equipe e plano de negócios para atender às demandas futuras.

  > [!TIP]
  > Agora inclui nativo de pontuação de modelos de Python!

+ [Executar o cliente clustering usando Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Saiba como usar o algoritmo Kmeans para executar o cluster sem supervisão de clientes.

## <a name="bkmk_Prerequisites"></a>Pré-requisitos

Para usar esses tutoriais, você deve ter instalado o SQL Server de 2017 Machine Learning Services (no banco de dados). 2017 do SQL Server dá suporte a R ou Python. No entanto, você deve instalar o framework de extensibilidade que suporta o aprendizado de máquina e selecione Python como o idioma a instalar. Você pode instalar o R e Python no mesmo computador.

> [!NOTE]
>
> Suporte para Python é um novo recurso do SQL Server 2017 e requer CTP 2.0 ou posterior. Embora o recurso está em pré-lançamento e não tem suporte para ambientes de produção, você está convidado a experimentá-lo e enviar seus comentários.

**SQL Server 2017**

Depois de executar a instalação do SQL Server, não se esqueça destas etapas importantes:

+ Habilitar o recurso de execução do script externo executando `sp_configure 'external scripts enabled', 1`.
+ Reinicie o servidor.
+ Verifique se o serviço que chama o tempo de execução externo tem as permissões necessárias.
+ Certifique-se de que o logon do SQL ou a conta de usuário do Windows tem as permissões necessárias para se conectar ao servidor, a leitura de dados e para criar os objetos de banco de dados necessários para o exemplo.

Se você tiver problemas, consulte este artigo para alguns problemas comuns: [Solucionando problemas de serviços de aprendizado de máquina](../machine-learning-troubleshooting-faq.md)

## <a name="see-also"></a>Consulte também

[Tutoriais de R para SQL Server](sql-server-r-tutorials.md)
