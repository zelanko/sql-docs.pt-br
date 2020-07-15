---
title: Opção de configuração de servidor External Scripts Enabled
description: Saiba mais sobre a opção de scripts externos habilitados no SQL Server. Depois de ativá-la, você pode executar scripts externos em linguagens com suporte, como R ou Python.
ms.date: 06/30/2020
ms.prod: sql
ms.technology: machine-learning-services
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- external scripts enabled
- external_scripts_enabled_TSQL
helpviewer_keywords:
- external scripts enabled option
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3915ca28aa6512c52e2cb465528bb4c04ea8dd21
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772489"
---
# <a name="external-scripts-enabled-server-configuration-option"></a>Opção de configuração de servidor External Scripts Enabled
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Use a opção **external scripts enabled** para habilitar a execução de scripts com certas extensões de linguagens remotas. Essa propriedade está DESATIVADA por padrão. Quando os **Serviços de Machine Learning** estiverem instalados, opcionalmente, a instalação poderá definir essa propriedade como true.

## <a name="remarks"></a>Comentários

É necessário habilitar a opção external script enabled para poder executar um script externo usando o procedimento [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) . Use **sp_execute_external_script** para executar scripts escritos em uma linguagem compatível, tal como R ou Python. 

+ Para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]

    [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] inclui suporte para a linguagem R no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e um conjunto de ferramentas de estação de trabalho e bibliotecas de conectividade de R.

    Instale o recurso **R Services** durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar a execução de scripts escritos em R.

+ Para [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] e posterior

    [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] tem suporte para as linguagens R e Python.

    Instale o recurso **Serviços de Machine Learning** durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar a execução de scripts externos. Verifique se você selecionou pelo menos um idioma durante a instalação inicial: R, Python ou ambos.

## <a name="additional-requirements"></a>Requisitos adicionais

Após a configuração, para habilitar scripts externos, execute o script a seguir:

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

Para obter mais informações, confira [Instalar os Serviços de Machine Learning do SQL Server (Python e R) no Windows](../../machine-learning/install/sql-machine-learning-services-windows-install.md) ou no [Linux](../../linux/sql-server-linux-setup-machine-learning-docker.md?toc=/sql/machine-learning/toc.json).

## <a name="see-also"></a>Confira também

+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
+ [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)
+ [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [Documentação do machine learning do SQL](../../machine-learning/index.yml)
