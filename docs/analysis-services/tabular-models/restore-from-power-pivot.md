---
title: Restaurar do Power Pivot | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql11.asvs.ssmsimbi.RestoreFromPP.f1
ms.assetid: 232ac8ed-77fe-47d8-acd3-59bc2fdfdf48
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 18c9eef295ca51648ce0dc27e94b9581ba353772
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="restore-from-power-pivot"></a>Restaurar do Power Pivot
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Você pode usar o recurso Restaurar do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no SQL Server Management Studio para criar um novo modelo de banco de dados de Tabela em uma instância do Analysis Services (executando em modo de Tabela) ou restaurar para um banco de dados existente de uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (.xlsx).  
  
> [!NOTE]  
>  O modelo de projeto Importar do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no SQL Server Data Tools fornece funcionalidade semelhante. Para obter mais informações, consulte [importar do PowerPivot](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md).  
  
 Ao usar Restaurar do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], tenha em mente o seguinte:  
  
-   Para usar o recurso Restaurar do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], você deverá estar conectado como membro da função Administradores de Servidor na instância do Analysis Services.  
  
-   A conta de serviço da instância do Analysis Services deve ter permissões de leitura no arquivo da pasta de trabalho que você está restaurando.  
  
-   Por padrão, quando você restaura um banco de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], a propriedade Informações de Representação da Fonte de Dados do banco de dados modelo de tabela é definida como padrão, que especifica a conta de serviço da instância do Analysis Services. É recomendável alterar as credenciais de representação para uma conta de usuário do Windows em Propriedades do Banco de Dados. Para obter mais informações, consulte [representação](../../analysis-services/tabular-models/impersonation-ssas-tabular.md).  
  
-   Os dados no modelo de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] serão copiados para um banco de dados modelo de tabela novo ou existente na instância do Analysis Services. Se sua pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] contiver tabelas vinculadas, elas serão recriadas como uma tabela sem uma fonte de dados, semelhante a uma tabela criada usando Colar em nova tabela.  
  
### <a name="to-restore-from-power-pivot"></a>Para restaurar do Power Pivot  
  
1.  No SSMS, na instância do Active Directory para a qual você quer restaurar, clique com o botão direito do mouse em **Bancos de dados** e clique em **Restaurar do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
2.  Na caixa de diálogo **Restaurar do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**, em **Restaurar Origem**, em **Arquivo de backup**, clique em **Procurar** e selecione um arquivo .abf ou .xslx do qual restaurar.  
  
3.  Em **Destino da Restauração**, em **Restaurar banco de dados**, digite um nome de um banco de dados novo ou existente. Se você não especificar um nome, o nome da pasta de trabalho será usado.  
  
4.  Em **Local de armazenamento**, clique em **Procurar**e selecione um local para armazenar o banco de dados.  
  
5.  Em **Opções**, deixe **Incluir informações de segurança** marcado. Ao restaurar de uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , essa configuração não se aplica.  
  
## <a name="see-also"></a>Consulte também  
 [Bancos de dados de modelo de tabela](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)   
 [Importar do Power Pivot](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)  
  
  
