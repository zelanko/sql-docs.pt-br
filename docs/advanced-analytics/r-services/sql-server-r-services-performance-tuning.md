---
title: "Ajuste de desempenho de servi&#231;os do SQL Server R | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf6f3b7d-f9f9-4e45-b0d1-07850b53e0c5
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# Ajuste de desempenho de servi&#231;os do SQL Server R
[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] fornece uma plataforma para desenvolvimento de aplicativos inteligentes que descobrem novas informações. Um cientista de dados pode usar o poder da linguagem R para treinar e criar modelos usando dados armazenados em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Quando o modelo estiver pronto para produção, um cientista de dados pode trabalhar com os administradores de banco de dados e engenheiros do SQL para implantar sua solução em produção. As informações nesta seção fornecem diretrizes de nível alto sobre ajuste de desempenho durante a criação e treinamento de modelos e durante a implantação de modelos para a produção.

As informações neste documento pressupõem que você esteja familiarizado com [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] conceitos e terminologia. Para obter informações gerais sobre os serviços de R, consulte [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md).

> [!NOTE]
> Embora grande parte das informações desta seção é orientação geral sobre como configurar [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], algumas informações são específicas para funções analíticas RevoScaleR.

## Nesta seção

* [Configuração do SQL Server](../../advanced-analytics/r-services/sql-server-configuration-r-services.md): este documento fornece orientação para a configuração de hardware que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] está instalado. É mais útil __administradores de banco de dados__.

* [R e otimização de dados](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md): este documento fornece orientação sobre como usar scripts R com os serviços de R. É mais útil __cientistas de dados__.

* [Estudo de caso de desempenho](../../advanced-analytics/r-services/performance-case-study-r-services.md): este documento fornece dados de teste e scripts de R que podem ser usados para testar o impacto da orientação fornecida nos documentos anteriores.

## Referências

Estes são links para informações usadas no desenvolvimento deste documento.

* [Como determinar o tamanho do arquivo de página apropriada para versões de 64 bits do Windows](https://support.microsoft.com/kb/2860880)

* [Compactação de dados](../../relational-databases/data-compression/data-compression.md)

* [Permitir a compactação em uma tabela ou índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

* [Desabilitar a compactação em uma tabela ou índice](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

* [Ferramenta de teste do DISKSPD armazenamento load generator e desempenho](https://github.com/microsoft/diskspd)

* [Referência de utilitário FSUtil](https://technet.microsoft.com/library/cc753059.aspx)

* [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

* [R Services](../../advanced-analytics/r-services/r-services.md)

* [Opções de ajuste de desempenho para rxDForest e rxDTree](https://support.microsoft.com/kb/3104235)

* [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)

* [Guia do usuário RevoScaleR](https://packages.revolutionanalytics.com/doc/7.0.0/win/RevoScaleR_Users_Guide.pdf)

* [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)

## Consulte também

 
 [Configuração do SQL Server para serviços de R](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [Estudo de caso de desempenho](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 
 [R e otimização de dados](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)