---
title: Exportar e importar objetos de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [Analysis Services]
- exporting mining models
- exporting mining structures
- mining structures [Analysis Services], creating
- mining structures [DMX], exporting
- mining models [Analysis Services], migration
ms.assetid: 10a83b13-2640-4ff5-80c8-a35e1d692908
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c2f79f8bf9a1d0ff01ba97d29662fab026d4adcd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084467"
---
# <a name="export-and-import-data-mining-objects"></a>Exportar e importar objetos de mineração de dados
  Além da funcionalidade fornecida no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para soluções de backup, restauração e migração, a Mineração de Dados do SQL Server fornece a capacidade de transferir rapidamente estruturas e modelos de mineração de dados entre servidores diferentes usando extensões DMX.  
  
 Se a sua solução de mineração de dados usar dados relacionais, em vez de um banco de dados multidimensional, a transferência de modelos com o uso de `EXPORT` e `IMPORT` será muito mais rápida e fácil do que com o uso da restauração do banco de dados ou da implantação de uma solução inteira.  
  
 Esta seção fornece uma visão geral de como transferir estruturas de mineração de dados e modelos usando instruções DMX. Para obter detalhes sobre a sintaxe, junto com exemplos, consulte [EXPORT &#40;DMX&#41;](/sql/dmx/export-dmx) e [IMPORT &#40;DMX&#41;](/sql/dmx/import-dmx).  
  
> [!NOTE]  
>  Você deve ser um administrador de banco de dados ou servidor para exportar ou importar objetos de um banco de dados do Microsoft SQL Server Analysis Services.  
  
## <a name="exporting-data-mining-structures"></a>Exportando estruturas de mineração de dados  
 Quando você exporta uma estrutura de mineração, a instrução EXPORT exporta todos os modelos associados automaticamente. Se você quiser controlar os objetos que são exportados, especifique cada objeto pelo nome.  
  
 Se a estrutura de mineração tiver sido processada e os resultados armazenados em cache, o que é o comportamento padrão, quando você exportar a estrutura de mineração, a definição conterá um resumo dos dados nos quais a estrutura se baseia. Para remover esse resumo, você deve limpar o cache associado com a estrutura de mineração executando uma operação `Process Clear Structure`. Para obter mais informações, consulte [Processar uma estrutura de mineração](process-a-mining-structure.md).  
  
### <a name="exporting-data-mining-models"></a>Exportando modelos de mineração de dados  
 Você pode usar a palavra-chave `WITH DEPENDENCIES` para exportar a fonte de dados e a definição de exibição da fonte de dados junto com o modelo de mineração e sua estrutura.  
  
 Quando você exportar um modelo de mineração sem exportar dependências, a instrução EXPORT exportará a definição do modelo de mineração e sua estrutura de mineração, mas não a definição das fontes de dados. Em virtude disso, após a importação do modelo, você poderá percorrê-lo imediatamente, mas se quiser reprocessar o modelo de mineração no servidor de destino ou executar consultas nos dados subjacentes, será necessário criar uma fonte de dados correspondente no servidor de destino.  
  
## <a name="importing-data-mining-structures-and-models"></a>Importando estruturas e modelos de mineração de dados  
 Quando um objeto de mineração de dados é importado, esse objeto é importado para o servidor e o banco de dados em que você está conectado durante a execução da instrução IMPORT. Se o arquivo de importação incluir um banco de dados não existente no servidor, o banco de dados será criado.  
  
 Você também pode importar uma estrutura de mineração ou modelo de mineração usando o comando `Restore`. As estruturas ou os modelos serão restaurados no banco de dados que tem o mesmo nome do banco de dados do qual foram exportados. Para obter mais informações, consulte [Opções de restauração](../multidimensional-models/restore-options.md).  
  
## <a name="remarks"></a>Comentários  
 Você não poderá importar uma estrutura ou modelo para um servidor se já houver um desses itens com o mesmo nome no servidor. Além disso, não é possível exportar um objeto de mineração de dados e depois modificar seu nome no arquivo de exportação. Assim, se você antecipar conflitos de nome, exclua o objeto de mineração de dados no servidor de destino ou renomeie esse objeto antes de exportar a definição.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento de soluções de mineração de dados e objetos](management-of-data-mining-solutions-and-objects.md)  
  
  
