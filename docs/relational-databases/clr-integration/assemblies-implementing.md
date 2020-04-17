---
title: Implementando Assembléias | Microsoft Docs
description: Saiba como trabalhar com conjuntos hospedados no SQL Server, incluindo como criar/modificar conjuntos, soltar ou ativar/desativar conjuntos e gerenciar versões.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], implementing
ms.assetid: c228d7bf-a906-4f37-a057-5d464d962ff8
author: rothja
ms.author: jroth
ms.openlocfilehash: 807ed6a6f0d59444cd38f7fdf902a7c3fc1b47d8
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488037"
---
# <a name="assemblies---implementing"></a>Assemblies – implementar
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico fornece informações sobre as seguintes áreas para ajudá-lo a implementar e trabalhar com assemblies no banco de dados:  
  
-   Criando assemblies  
  
-   Modificando assemblies  
  
-   Queda, desativação e ativação de assembléias  
  
-   Gerenciamento de versões de montagem  
  
## <a name="creating-assemblies"></a>Criando Assemblies  
 Os assemblies são criados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando o Assembly Assisted Editor. Além disso, a implantação de um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Projeto sql server registra uma montagem no banco de dados especificada para o projeto. Para obter mais informações, consulte [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md).  
  
 **Para criar um assembly usando o Transact-SQL**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
 **Para criar um assembly usando o SQL Server Management Studio**  
  
-   [Propriedades de montagem &#40;página geral&#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="modifying-assemblies"></a>Modificando assembléias  
 Os assemblies são modificados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a instrução ALTER ASSEMBLY [!INCLUDE[tsql](../../includes/tsql-md.md)] ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando o Assembly Assisted Editor. Você pode modificar um assembly quando quiser fazer o seguinte:  
  
-   Altere a implementação do assembly carregando uma versão mais nova dos binários do assembly. Para obter mais informações, consulte [Gerenciar versões de montagem](#_managing) mais tarde neste tópico.  
  
-   Altere o conjunto de permissões do assembly. Para obter mais informações, confira [Criando assemblies](../../relational-databases/clr-integration/assemblies-designing.md).  
  
-   Altere a visibilidade do assembly. Assemblies visíveis estão disponíveis para consulta no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Assemblies não visíveis não estão disponíveis, mesmo se tiverem sido carregados no banco de dados. Por padrão, os assemblies carregados para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são visíveis.  
  
-   Adicione ou descarte um arquivo de depuração ou de origem associado ao assembly.  
  
 **Para modificar um assembly usando o Transact-SQL**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
 **Para modificar um assembly usando o SQL Server Management Studio**  
  
-   [Propriedades de montagem &#40;página geral&#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="dropping-disabling-and-enabling-assemblies"></a>Descartando, desabilitando e habilitando assemblies  
 Os assemblies são descartados usando a instrução DROP ASSEMBLY [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Para descartar um assembly usando o Transact-SQL**  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **Para descartar um assembly usando o SQL Server Management Studio**  
  
-   [Excluir Objetos](../../ssms/object/delete-objects.md)  
  
 Por padrão, todos os assemblies que são criados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão desabilitados para execução. Você pode usar a opção **habilitada clr** do procedimento armazenado **no sistema sp_configure** para desativar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou habilitar a execução de todos os conjuntos que são carregados em . Desabilitar a execução de assemblies impede que funções CLR (Common Language Runtime), procedimentos armazenados, gatilhos, agregações e tipos definidos pelo usuário sejam executados e interrompe os que estão sendo executados no momento. A desabilitação da execução do assembly não desabilita a capacidade de criar, alterar ou descartar assemblies. Para obter mais informações, consulte [a opção de configuração do servidor habilitada clr](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md).  
  
 **Para desabilitar e habilitar a execução de assemblies**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
##  <a name="managing-assembly-versions"></a><a name="_managing"></a>Gerenciamento de versões de montagem  
 Quando um assembly é carregado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o assembly é armazenado e gerenciado dentro dos catálogos do sistema de banco de dados. Quaisquer alterações feitas na definição [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] da montagem no deve ser propagada para a montagem que está armazenada no catálogo do banco de dados.  
  
 Quando for preciso modificar um assembly, você deverá emitir uma instrução ALTER ASSEMBLY para atualizar o assembly no banco de dados. Isso atualizará o assembly até a última cópia de módulos do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que contenha sua implementação.  
  
 A cláusula WITH UNCHECKED DATA da instrução ALTER ASSEMBLY instrui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para atualizar até mesmo os assemblies dos quais os dados persistentes no banco de dados sejam dependentes. Especificamente, você deve especificar WITH UNCHECKED DATA se qualquer uma dessas opções existir:  
  
-   Colunas computadas persistentes que referenciem métodos no assembly, seja direta ou indiretamente, através de funções ou métodos [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   As colunas de um tipo de dado CLR definido pelo usuário que dependem do assembly e o tipo implementa um formato de serialização **UserDefined** (não **nativo**).  
  
> [!CAUTION]  
>  Se WITH UNCHECKED DATA não for especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentará impedir que ALTER ASSEMBLY seja executada se a nova versão do assembly afetar dados existentes em tabelas, índices ou outros locais persistentes. Porém, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não garante que colunas computadas, índices, exibições indexadas ou expressões sejam consistentes com as rotinas e tipos subjacentes quando o assembly CLR for atualizado. Tenha cuidado ao executar ALTER ASSEMBLY, para ter certeza de que não haja nenhuma desigualdade entre o resultado de uma expressão e um valor que é baseado naquela expressão armazenado no assembly.  
  
 Somente membros da função de banco de dados **fixo db_owner** e **db_ddlowner** podem executar a MONTAGEM ALTER usando a cláusula DADOS NÃO MARCADOS.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publica uma mensagem no log de eventos de aplicativos do Windows informando que o assembly foi modificado com dados não verificados nas tabelas. Em seguida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] marca qualquer tabela que contenha dados dependentes do assembly como tendo dados não verificados. A **has_unchecked_assembly_data** coluna da exibição do catálogo **sys.tables** contém o valor 1 para tabelas que contêm dados não verificados e 0 para tabelas sem dados não verificados.  
  
 Para resolver a integridade dos dados não verificados, execute DBCC CHECKDB COM EXTENDED_LOGICAL_CHECKS contra cada tabela que tenha dados não verificados. Se dbcc checkdb com EXTENDED_LOGICAL_CHECKS falhar, você deve excluir as linhas de tabela que não são válidas ou modificar o código de montagem para resolver problemas e, em seguida, emitir instruções adicionais ALTER ASSEMBLY.  
  
 ALTER ASSEMBLY altera a versão do assembly. A cultura e o símbolo de chave pública da assembléia permanecem os mesmos. O SQL Server não permite registrar diferentes versões de um conjunto com o mesmo nome, cultura e chave pública.  
  
### <a name="interactions-with-computer-wide-policy-for-version-binding"></a>Interações com a política de computadores para associação de versões  
 Se as referências a assemblies armazenadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forem redirecionadas a versões específicas usando política de publicador ou política de administrador de computadores, você deve agir de uma das seguintes maneiras:  
  
-   Verificar se a nova versão para a qual esse redirecionamento é feito está no banco de dados.  
  
-   Modificar qualquer instrução dos arquivos de política externa do computador ou de política de publicador para ter certeza de que fazem referência à versão específica que está no banco de dados.  
  
 Caso contrário, uma tentativa para carregar uma nova versão de assembly à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] falhará.  
  
 **Para atualizar a versão de um assembly**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;do mecanismo de banco de dados &#40;conjuntos](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Obtendo informações sobre assemblies](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
