---
title: "Filtrar dados antes de exportar (suplemento MDS para Excel) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9e30eae0-776b-4a09-aac3-0c0249d92ca5
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# Filtrar dados antes de exportar (suplemento MDS para Excel)
  Em [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], filtrar dados quando você deseja limitar o tamanho ou o escopo dos dados que você está exportando para o Excel.  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
### Para filtrar dados antes de exportar  
  
1.  Abra o Excel e, na guia **Dados Mestre** , conecte-se a um repositório do MDS. Para obter mais informações, consulte [conectar-se a um repositório do MDS & #40. Suplemento do MDS para Excel e 41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md).  
  
2.  No painel do **Master Data Explorer** , selecione um modelo e uma versão. A lista de entidades será preenchida.  
  
    -   Se o painel do **Master Data Explorer** não estiver visível, no grupo **Conectar e Carregar** , clique em **Mostrar Explorer**.  
  
    -   Se o **Master Data Explorer** painel está desabilitado, é porque a planilha existente já contém dados gerenciados no MDS. Para habilitar o painel, abra uma nova planilha.  
  
3.  No **Master Data Explorer** painel, na lista de entidades, clique na entidade que você deseja filtrar.  
  
4.  Na faixa de opções, no **conectar e carregar** clique em **filtro**.  
  
5.  Conclua o **filtro** caixa de diálogo selecionando os atributos (colunas) para exibir, definindo a ordem das colunas e, se necessário, filtrando os dados para menos linhas sejam retornadas. Exibição de **Resumo** painel para a quantidade de dados será retornado. Para obter mais informações, consulte [caixa de diálogo Filtro & #40. Suplemento do MDS para Excel e 41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md).  
  
6.  Clique em **Carregar Dados**. A planilha será preenchida com os dados gerenciados no MDS.  
  
    > [!NOTE]  
    >  -   Somente os primeiros um milhão de membros serão carregados no Excel.  
    > -   Nas colunas que são listas restritas (atributos baseados em domínio), por padrão, somente os primeiros 25000 valores serão carregados.  
  
## Próximas etapas  
 [Importar dados do Excel para Master Data Services & #40. Suplemento do MDS para Excel e 41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## Consulte também  
 [Visão geral: Exportando dados para o Excel e 40; Suplemento do MDS para Excel e 41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [Caixa de diálogo Filtro & #40. Suplemento do MDS para Excel e 41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)   
 [Reordenar colunas & #40. Suplemento do MDS para Excel e 41;](../../master-data-services/microsoft-excel-add-in/reorder-columns-mds-add-in-for-excel.md)  
  
  