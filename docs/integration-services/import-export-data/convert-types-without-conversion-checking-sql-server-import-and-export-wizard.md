---
title: "Converter tipos sem verifica&#231;&#227;o de convers&#227;o (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "01/11/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.nomappingfile.f1"
ms.assetid: 87d9d3e5-477f-4117-a37f-bff53ea3e14d
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Converter tipos sem verifica&#231;&#227;o de convers&#227;o (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server)
  Depois de selecionar as tabelas existentes e exibições para copiar ou examinar a consulta que você forneceu, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode mostrar **Converter tipos sem verificar a conversão**. O assistente mostra essa página quando não é possível localizar um ou mais dos arquivos de mapeamento e de conversão de tipo de dados necessários para mapear os tipos de dados entre a origem e o destino. A página inclui informações que ajudam você a compreender o que está faltando.
  
 Clique em **Avançar** para continuar sem saber se as conversões de tipo de dados serão bem-sucedidas. Caso contrário, clique em **Voltar** para alterar suas seleções ou clique em **Cancelar** para sair do assistente.
  
 Para obter informações sobre como o assistente mapeia tipos de dados de colunas de origem para colunas de destino e sobre como o assistente usa os arquivos de mapeamento de tipo de dados, consulte [Como o assistente mapeia tipos de dados entre a origem e o destino?](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardMapping).  

## <a name="screen-shot-of-the-convert-types-page"></a>Captura de tela da página Converter Tipos  
  
A captura de tela a seguir mostra um exemplo da página **Converter Tipos sem Verificar a Conversão** do Assistente.

![Converter tipos](../../integration-services/import-export-data/media/convert-types.png)

O problema aqui é que o assistente não pode encontrar um arquivo de mapeamento que mapeia tipos de dados para o destino selecionado.

As informações desta página não incluem o nome do arquivo de mapeamento ausente. Como o assistente não sabe se um arquivo existe para o provedor de dados especificado, ele não pode fornecer um nome para o arquivo ausente.

## <a name="whats-next"></a>O que vem a seguir?  
 Após clicar em **Avançar** para continuar sem saber se as conversões de tipo de dados serão bem-sucedidas, a próxima página será **Salvar e Executar o Pacote**. Nesta página, especifique se deseja executar a operação de cópia imediatamente. Dependendo da sua configuração, você também poderá salvar o pacote do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criado pelo assistente para personalizá-lo e reutilizá-lo posteriormente. Para obter mais informações, consulte [Salvar e Executar o Pacote](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  
