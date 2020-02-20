---
title: Usar o T-SQL (CRIAR BIBLIOTECA EXTERNA) para instalar pacotes de R
description: Adicione novos pacotes de R ao SQL Server 2016 R Services ou Serviços de Machine Learning do SQL Server (no banco de dados).
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/20/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: =sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: b19b2df1b39bcc88332d60f1389be12b32d7b921
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74485261"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server"></a>Use o T-SQL (CRIAR BIBLIOTECA EXTERNA) para instalar pacotes de R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo explica como instalar novos pacotes de R em uma instância do SQL Server em que o Machine Learning está habilitado. Há várias abordagens para escolher. O uso do T-SQL funciona melhor para os administradores de servidor que não estão familiarizados com R.

**Aplicável a:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

A instrução [CRIAR BIBLIOTECA EXTERNA](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) torna possível adicionar um pacote ou conjunto de pacotes a uma instância ou um banco de dados específico sem executar o código R ou Python diretamente. No entanto, esse método requer permissões de banco de dados adicionais e preparação de pacote.

+ Todos os pacotes devem estar disponíveis como um arquivo compactado local, em vez de baixados sob demanda da Internet.

+ Todas as dependências devem ser identificadas por nome e versão e incluídas no arquivo zip. A instrução falhará se os pacotes necessários não estiverem disponíveis, incluindo dependências de pacote downstream. 

+ Você deve ser o **db_owner** ou ter a permissão de CRIAR BIBLIOTECA EXTERNA em uma função de banco de dados. Para obter detalhes, confira [CRIAR BIBLIOTECA EXTERNA](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="download-packages-in-archive-format"></a>Baixar pacotes no formato de arquivos

Se você está instalando um só pacote, baixe o pacote no formato compactado.

É mais comum instalar múltiplos pacotes devido a dependências de pacote. Quando um pacote requer outros pacotes, você deve verificar se todos eles estão acessíveis entre si durante a instalação. É recomendável [criar um repositório local](create-a-local-package-repository-using-minicran.md) usando [miniCRAN](https://andrie.github.io/miniCRAN/) para montar uma coleção completa de pacotes, bem como [igraph](https://igraph.org/r/) para analisar dependências de pacotes. A instalação da versão errada de um pacote ou a omissão de uma dependência de pacote pode causar uma falha na instrução CRIAR BIBLIOTECA EXTERNA. 

## <a name="copy-the-file-to-a-local-folder"></a>Copie o arquivo para uma pasta local

Copie o arquivo compactado que contém todos os pacotes para uma pasta local no servidor. Se você não tiver acesso ao sistema de arquivos no servidor, também poderá passar um pacote completo como uma variável, usando um formato binário. Para obter mais informações, confira [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md).

## <a name="run-the-statement-to-upload-packages"></a>Executar a instrução para carregar pacotes

Abra uma janela de **Consulta**, usando uma conta com privilégios administrativos.

Execute a instrução T-SQL `CREATE EXTERNAL LIBRARY` para carregar a coleção de pacotes compactados no banco de dados.

Por exemplo, a instrução a seguir nomeia como a origem do pacote um repositório miniCRAN que contém o pacote **randomForest**, junto com suas dependências. 

```sql
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

Você não pode usar um nome aleatório; o nome da biblioteca externa deve ter o mesmo nome que você pretende usar ao carregar ou chamar o pacote.

## <a name="verify-package-installation"></a>Verificar a instalação do pacote

Se a biblioteca for criada com êxito, você poderá executar o pacote no SQL Server, chamando-o dentro de um procedimento armazenado.
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>Confira também

+ [Obter informações sobre o pacote do R](r-package-information.md)
+ [Tutoriais do R](../tutorials/sql-server-r-tutorials.md)