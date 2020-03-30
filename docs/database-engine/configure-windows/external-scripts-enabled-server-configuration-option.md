---
title: Opção de configuração de servidor External Scripts Enabled | Microsoft Docs
ms.date: 11/13/2017
ms.prod: sql
ms.technology: configuration
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- external scripts enabled
- external_scripts_enabled_TSQL
helpviewer_keywords:
- external scripts enabled option
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3f47352cc82ac831ebcd64548baa24423490094f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72006051"
---
# <a name="external-scripts-enabled-server-configuration-option"></a>Opção de configuração de servidor External Scripts Enabled
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
**Aplica-se a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] e [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

Use a opção **external scripts enabled** para habilitar a execução de scripts com certas extensões de linguagens remotas. Essa propriedade está DESATIVADA por padrão. Quando os **Serviços de Análise Avançada** estiverem instalados, opcionalmente, a instalação poderá definir essa propriedade como true.

## <a name="remarks"></a>Comentários

É necessário habilitar a opção external script enabled para poder executar um script externo usando o procedimento [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) . Use **sp_execute_external_script** para executar scripts escritos em uma linguagem compatível, tal como R ou Python. 

+ Para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]

    [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] inclui suporte para a linguagem R no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e um conjunto de ferramentas de estação de trabalho e bibliotecas de conectividade de R.

    Instale o recurso **Extensões de Análise Avançada** durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar a execução de scripts escritos em R. A linguagem R é instalada por padrão.

+ Para [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]

    [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] usa a mesma arquitetura de SQL Server 2016, mas dá suporte à linguagem Python.

    Instale o recurso **Extensões de Análise Avançada** durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar a execução de scripts externos. Verifique se você selecionou pelo menos um idioma durante a instalação inicial: R, Python ou ambos. 

## <a name="additional-requirements"></a>Requisitos adicionais

Após a configuração, para habilitar scripts externos, execute o script a seguir:

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

Você deve reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para efetivar a alteração.

Para obter mais informações, consulte [Configurar o SQL Server Machine Learning](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).

## <a name="see-also"></a>Confira também

[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)

[RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)

[sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

[Serviços de Machine Learning do SQL Server](../../advanced-analytics/r/sql-server-r-services.md)
