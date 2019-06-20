---
title: Implementando Assemblies | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], implementing
ms.assetid: c228d7bf-a906-4f37-a057-5d464d962ff8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dc1bfce77a089b24e68613c94af6e2886e6b5952
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874466"
---
# <a name="implementing-assemblies"></a>Implementando assemblies
  Este tópico fornece informações sobre as seguintes áreas para ajudá-lo a implementar e trabalhar com assemblies no banco de dados:  
  
-   Criando assemblies  
  
-   Modificando assemblies  
  
-   Descartando, desabilitando e habilitando assemblies  
  
-   Gerenciando versões de assembly  
  
## <a name="creating-assemblies"></a>Criando Assemblies  
 Os assemblies são criados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando o Assembly Assisted Editor. Além disso, a implantação de um projeto do SQL Server no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra um assembly no banco de dados que foi especificado para o projeto. Para obter mais informações, consulte [Deploying CLR Database Objects](deploying-clr-database-objects.md).  
  
 **Para criar um assembly usando o Transact-SQL**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
 **Para criar um assembly usando o SQL Server Management Studio**  
  
-   [Propriedades do assembly &#40;página geral&#41;](assemblies-properties.md)  
  
## <a name="modifying-assemblies"></a>Modificando Assemblies  
 Os assemblies são modificados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a instrução ALTER ASSEMBLY [!INCLUDE[tsql](../../includes/tsql-md.md)] ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando o Assembly Assisted Editor. Você pode modificar um assembly quando quiser fazer o seguinte:  
  
-   Altere a implementação do assembly carregando uma versão mais nova dos binários do assembly. Para obter mais informações, consulte [gerenciando versões de Assembly](#_managing) mais adiante neste tópico.  
  
-   Altere o conjunto de permissões do assembly. Para obter mais informações, confira [Criando assemblies](../../relational-databases/clr-integration/assemblies-designing.md).  
  
-   Altere a visibilidade do assembly. Assemblies visíveis estão disponíveis para consulta no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Assemblies não visíveis não estão disponíveis, mesmo se tiverem sido carregados no banco de dados. Por padrão, os assemblies carregados para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são visíveis.  
  
-   Adicione ou descarte um arquivo de depuração ou de origem associado ao assembly.  
  
 **Para modificar um assembly usando o Transact-SQL**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
 **Para modificar um assembly usando o SQL Server Management Studio**  
  
-   [Propriedades do assembly &#40;página geral&#41;](assemblies-properties.md)  
  
## <a name="dropping-disabling-and-enabling-assemblies"></a>Descartando, desabilitando e habilitando assemblies  
 Os assemblies são descartados usando a instrução DROP ASSEMBLY [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Para descartar um assembly usando o Transact-SQL**  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **Para descartar um assembly usando o SQL Server Management Studio**  
  
-   [Excluir Objetos](../../ssms/object/delete-objects.md)  
  
 Por padrão, todos os assemblies que são criados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão desabilitados para execução. Você pode usar o **clr habilitado** opção do **sp_configure** sistema de procedimento armazenado para desabilitar ou habilitar a execução de todos os assemblies que são carregados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Desabilitar a execução de assemblies impede que funções CLR (Common Language Runtime), procedimentos armazenados, gatilhos, agregações e tipos definidos pelo usuário sejam executados e interrompe os que estão sendo executados no momento. A desabilitação da execução do assembly não desabilita a capacidade de criar, alterar ou descartar assemblies. Para obter mais informações, consulte [opção de configuração do servidor clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md).  
  
 **Para desabilitar e habilitar a execução de assembly**  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
##  <a name="_managing"></a> Gerenciando versões de Assembly  
 Quando um assembly é carregado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o assembly é armazenado e gerenciado dentro dos catálogos do sistema de banco de dados. Todas as alterações feitas à definição do assembly na [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] devem ser propagadas para o assembly que é armazenado no catálogo do banco de dados.  
  
 Quando for preciso modificar um assembly, você deverá emitir uma instrução ALTER ASSEMBLY para atualizar o assembly no banco de dados. Isso atualizará o assembly até a última cópia de módulos do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que contenha sua implementação.  
  
 A cláusula WITH UNCHECKED DATA da instrução ALTER ASSEMBLY instrui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para atualizar até mesmo os assemblies dos quais os dados persistentes no banco de dados sejam dependentes. Especificamente, você deve especificar WITH UNCHECKED DATA se qualquer uma dessas opções existir:  
  
-   Colunas computadas persistentes que referenciem métodos no assembly, seja direta ou indiretamente, através de funções ou métodos [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   As colunas de um tipo de dado CLR definido pelo usuário que dependem do assembly e o tipo implementa um formato de serialização **UserDefined** (não **nativo**).  
  
> [!CAUTION]  
>  Se WITH UNCHECKED DATA não for especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentará impedir que ALTER ASSEMBLY seja executada se a nova versão do assembly afetar dados existentes em tabelas, índices ou outros locais persistentes. Porém, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não garante que colunas computadas, índices, exibições indexadas ou expressões sejam consistentes com as rotinas e tipos subjacentes quando o assembly CLR for atualizado. Tenha cuidado ao executar ALTER ASSEMBLY, para ter certeza de que não haja nenhuma desigualdade entre o resultado de uma expressão e um valor que é baseado naquela expressão armazenado no assembly.  
  
 Somente os membros dos **db_owner** e **db_ddlowner** função fixa de banco de dados pode executar ALTER ASSEMBLY usando a cláusula WITH UNCHECKED DATA.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publica uma mensagem no log de eventos de aplicativos do Windows informando que o assembly foi modificado com dados não verificados nas tabelas. Em seguida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] marca qualquer tabela que contenha dados dependentes do assembly como tendo dados não verificados. O **has_unchecked_assembly_data** coluna o **sys. Tables** exibição do catálogo contém o valor 1 para tabelas que contêm dados não verificados e 0 para tabelas sem dados não verificados.  
  
 Para resolver a integridade de dados não verificados, execute DBCC CHECKTABLE em cada tabela que tiver dados não verificados. Se DBCC CHECKTABLE falhar, você terá de excluir as linhas da tabela que não sejam válidas ou modificar o código do assembly para tratar de problemas e, em seguida, emitir instruções ALTER ASSEMBLY adicionais.  
  
 ALTER ASSEMBLY altera a versão do assembly. A cultura e token de chave pública do assembly permanecem os mesmos. SQL Server não permite registrar versões diferentes de um assembly com o mesmo nome, cultura e chave pública.  
  
### <a name="interactions-with-computer-wide-policy-for-version-binding"></a>Interações com a política de computadores para associação de versões  
 Se as referências a assemblies armazenadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forem redirecionadas a versões específicas usando política de publicador ou política de administrador de computadores, você deve agir de uma das seguintes maneiras:  
  
-   Verificar se a nova versão para a qual esse redirecionamento é feito está no banco de dados.  
  
-   Modificar qualquer instrução dos arquivos de política externa do computador ou de política de publicador para ter certeza de que fazem referência à versão específica que está no banco de dados.  
  
 Caso contrário, uma tentativa para carregar uma nova versão de assembly à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] falhará.  
  
 **Para atualizar a versão de um assembly**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
## <a name="see-also"></a>Consulte também  
 [Assemblies &#40;mecanismo de banco de dados&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Obtendo informações sobre assemblies](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
