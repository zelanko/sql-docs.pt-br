---
title: ALTER ASSEMBLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_ASSEMBLY_TSQL
- ALTER ASSEMBLY
dev_langs:
- TSQL
helpviewer_keywords:
- assemblies [CLR integration], modifying
- refreshing assemblies
- assemblies [CLR integration], versioning
- assemblies [CLR integration], adding files
- modifying assemblies
- adding files
- ALTER ASSEMBLY statement
ms.assetid: 87bca678-4e79-40e1-bb8b-bd5ed8f34853
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c405884f8ff87cb0b37991dc5639bf69068a6ffd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52503095"
---
# <a name="alter-assembly-transact-sql"></a>ALTER ASSEMBLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Altera um assembly pela modificação das propriedades do catálogo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um assembly. ALTER ASSEMBLY o atualiza para a cópia mais recente dos módulos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que contêm sua implementação e adiciona ou remove os arquivos associados a ele. Os assemblies são criados usando [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md).  

>  [!WARNING]
>  O CLR usa o CAS (Segurança de Acesso do Código) no .NET Framework, para o qual não há mais suporte como um limite de segurança. Um assembly CLR criado com o `PERMISSION_SET = SAFE` pode conseguir acessar recursos externos do sistema, chamar um código não gerenciado e adquirir privilégios sysadmin. A partir do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], uma opção `sp_configure` chamada `clr strict security` é introduzida, a fim de aumentar a segurança de assemblies CLR. A `clr strict security` está habilitada por padrão e trata assemblies `SAFE` e `EXTERNAL_ACCESS` como se eles fossem marcados como `UNSAFE`. A opção `clr strict security` pode ser desabilitada para compatibilidade com versões anteriores, mas isso não é recomendado. A Microsoft recomenda que todos os assemblies sejam assinados por um certificado ou uma chave assimétrica com um logon correspondente que recebeu a permissão `UNSAFE ASSEMBLY` no banco de dados mestre. Para obter mais informações, consulte [Segurança estrita do CLR](../../database-engine/configure-windows/clr-strict-security.md).  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER ASSEMBLY assembly_name  
    [ FROM <client_assembly_specifier> | <assembly_bits> ]  
    [ WITH <assembly_option> [ ,...n ] ]  
    [ DROP FILE { file_name [ ,...n ] | ALL } ]  
    [ ADD FILE FROM   
    {   
        client_file_specifier [ AS file_name ]   
      | file_bits AS file_name   
    } [,...n ]   
    ] [ ; ]  
<client_assembly_specifier> :: =  
    '\\computer_name\share-name\[path\]manifest_file_name'  
  | '[local_path\]manifest_file_name'  
  
<assembly_bits> :: =  
    { varbinary_literal | varbinary_expression }  
  
<assembly_option> :: =  
    PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE }   
  | VISIBILITY = { ON | OFF }  
  | UNCHECKED DATA  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *assembly_name*  
 É o nome do assembly que você deseja modificar. *assembly_name* já precisa existir no banco de dados.  
  
 FROM \<client_assembly_specifier> | \<assembly_bits>  
 Atualiza um assembly à cópia mais recente dos módulos do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que contêm sua implementação. Esta opção pode ser usada somente se não houver nenhum arquivo associado ao assembly especificado.  
  
 \<client_assembly_specifier> especifica o local de rede ou a localização local onde reside o assembly que está sendo atualizado. O local da rede inclui o nome do computador, o nome do compartilhamento e um caminho dentro desse compartilhamento. *manifest_file_name* especifica o nome do arquivo que contém o manifesto do assembly.  

> [!IMPORTANT]
> O Banco de Dados SQL do Azure não é compatível com a referência a um arquivo.
  
 \<assembly_bits> é o valor binário do assembly.  
  
 Devem ser emitidas instruções ALTER ASSEMBLY separadas para qualquer assembly dependente que também requeira atualização.  
  
 PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE }   
>  [!IMPORTANT]  
>  A opção `PERMISSION_SET` é afetada pela opção `clr strict security`, descrita no aviso de abertura. Quando `clr strict security` está habilitada, todos os assemblies são tratados como `UNSAFE`.  
 Especifica a propriedade do conjunto de permissões de acesso ao código do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] do assembly. Para obter mais informações sobre essa propriedade, confira [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md).  
  
> [!NOTE]  
>  As opções EXTERNAL_ACCESS e UNSAFE não estão disponíveis em um banco de dados contido.  
  
 VISIBILITY = { ON | OFF }  
 Indica se o assembly está visível para a criação de funções CLR (Common Language Runtime), procedimentos armazenados, disparadores, tipos de dados definidos pelo usuário e funções de agregação definidas pelo usuário em relação a ele. Se for definido como OFF, o assembly foi projetado para ser chamado somente por outros assemblies. Se houver objetos de banco de dados CLR existentes já criados em relação ao assembly, a visibilidade do assembly não poderá ser alterada. Todos os assemblies referenciados por *assembly_name* são carregados como não visíveis por padrão.  
  
 UNCHECKED DATA  
 Por padrão, ALTER ASSEMBLY falhará se deve verificar a consistência de linhas de tabela individuais. Esta opção permite adiar as verificações com o uso de DBCC CHECKTABLE. Se for especificada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executará a instrução ALTER ASSEMBLY mesmo se houver tabelas no banco de dados que contenham o seguinte:  
  
-   Colunas computadas persistentes que referenciem métodos no assembly, direta ou indiretamente, por meio de funções ou métodos [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Restrições CHECK que referenciam métodos no assembly direta ou indiretamente.  
  
-   As colunas de um tipo de dado CLR definido pelo usuário que dependem do assembly e o tipo implementa um formato de serialização **UserDefined** (não **nativo**).  
  
-   Colunas de um tipo CLR definido pelo usuário que fazem referência a exibições criadas com o uso de WITH SCHEMABINDING.  
  
 Se quaisquer restrições CHECK estiverem presentes, elas serão desabilitadas e marcadas como não confiáveis. Quaisquer tabelas que contenham colunas dependentes do assembly serão marcadas como contendo dados não verificados até que essas tabelas sejam verificadas explicitamente.  
  
 Somente membros das funções de banco de dados fixas **db_owner** e **db_ddlowner** podem especificar essa opção.  
  
 A permissão **ALTER ANY SCHEMA** é necessária para especificar essa opção.  
  
 Para obter mais informações, confira [Implementando assemblies](../../relational-databases/clr-integration/assemblies-implementing.md).  
  
 [ DROP FILE { *file_name*[ **,**_...n_] | ALL } ]  
 Remove do banco de dados o nome de arquivo associado ao assembly ou todos os arquivos associados ao assembly. Se for usado com ADD FILE a seguir, DROP FILE será executado em primeiro lugar. Isto permite que você substitua um arquivo com o mesmo nome de arquivo.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente nem no Banco de Dados SQL do Azure.  
  
 [ ADD FILE FROM { *client_file_specifier* [ AS *file_name*] | *file_bits*AS *file_name*}  
 Carrega um arquivo a ser associado ao assembly, como código-fonte, arquivos de depuração ou outras informações relacionadas, no servidor tornando-o visível na exibição de catálogo **assembly_files**. *client_file_specifier* especifica o local do qual o arquivo deve ser carregado. Nesse caso, *file_bits* pode ser usado para especificar a lista de valores binários que compõem o arquivo. *file_name* especifica o nome sob o qual o arquivo deve ser armazenado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *file_name* precisará ser especificado se *file_bits* for especificado e será opcional se *client_file_specifier* for especificado. Se *file_name* não for especificado, a parte file_name de *client_file_specifier* será usada como *file_name*.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente nem no Banco de Dados SQL do Azure.  
  
## <a name="remarks"></a>Remarks  
 ALTER ASSEMBLY não interrompe sessões que estejam atualmente em execução com código no assembly que está sendo modificado. As sessões atuais concluem a execução usando os bits inalterados do assembly.  
  
 Se a cláusula FROM for especificada, ALTER ASSEMBLY atualizará o assembly com relação às cópias mais recentes dos módulos fornecidos. Como pode haver funções CLR, procedimentos armazenados, disparadores, tipos de dados e funções de agregação definidas pelo usuário na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que já estejam definidos em relação ao assembly, a instrução ALTER ASSEMBLY os reassocia à implementação mais recente do assembly. Para realizar essa nova associação, os métodos mapeados para funções CLR, procedimentos armazenados e disparadores ainda deverão existir no assembly modificado com as mesmas assinaturas. As classes que implementam tipos CLR definidos pelo usuário e funções de agregação definidas pelo usuário ainda deverão satisfazer os requisitos para serem uma agregação ou tipo definido pelo usuário.  
  
> [!CAUTION]  
>  Se WITH UNCHECKED DATA não for especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentará impedir que ALTER ASSEMBLY seja executada se a nova versão do assembly afetar dados existentes em tabelas, índices ou outros locais persistentes. Entretanto, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não garante que colunas computadas, índices, exibições indexadas ou expressões serão consistentes com as rotinas e tipos subjacentes quando o assembly CLR for atualizado. Tenha cuidado ao executar ALTER ASSEMBLY, para ter certeza de que não haja uma incompatibilidade entre o resultado de uma expressão e um valor com base nessa expressão armazenado no assembly.  
  
 ALTER ASSEMBLY altera a versão do assembly. A cultura e o token de chave pública do assembly permanecem os mesmos.  
  
 A instrução ALTER ASSEMBLY não pode ser usada para alterar o seguinte:  
  
-   As assinaturas de funções CLR, funções de agregação, procedimentos armazenados e disparadores em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que façam referência ao assembly. ALTER ASSEMBLY falha quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não puder reassociar objetos de banco de dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a nova versão do assembly.  
  
-   As assinaturas de métodos no assembly que são chamados a partir de outros assemblies.  
  
-   A lista de assemblies que dependem do assembly, referenciada na propriedade do assembly **DependentList**.  
  
-   A capacidade de indexação de um método, a menos que não existam índices ou colunas computadas persistidas que dependam desse método, seja direta ou indiretamente.  
  
-   O atributo de nome de método **FillRow** para funções com valor de tabela do CLR.  
  
-   A assinatura de método **Accumulate** e **Terminate** para agregações definidas pelo usuário.  
  
-   Assemblies do sistema.  
  
-   Propriedade do assembly. Nesse caso, use [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 Além disso, para assemblies que implementam tipos definidos pelo usuário, ALTER ASSEMBLY pode ser usada para fazer somente as seguintes alterações:  
  
-   Modificar métodos públicos da classe de tipo definida pelo usuário, contanto que não sejam alterados assinaturas ou atributos.  
  
-   Adicionar novos métodos públicos.  
  
-   Modificar métodos privados de alguma forma.  
  
 Os campos contidos em um tipo definido pelo usuário serializado de forma nativa, incluindo membros de dados ou classes base, não podem ser alterados usando ALTER ASSEMBLY. Não é oferecido suporte a todas as demais alterações.  
  
 Se ADD FILE FROM não for especificado, ALTER ASSEMBLY descartará quaisquer arquivos associados ao assembly.  
  
 Se ALTER ASSEMBLY for executado sem a cláusula de dados UNCHECKED, serão executadas verificações para averiguar se a nova versão do assembly não afeta dados existentes em tabelas. Dependendo da quantidade de dados que precisa ser verificada, isso pode afetar o desempenho.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão ALTER no assembly. Os requisitos adicionais são os seguintes:  
  
-   Para alterar um assembly cujo conjunto de permissões existente seja EXTERNAL_ACCESS, a permissão **EXTERNAL ACCESS ASSEMBLY** será necessária no servidor.  
  
-   Para alterar um assembly cujo conjunto de permissões existente seja UNSAFE, a permissão **UNSAFE ASSEMBLY** será necessária no servidor.  
  
-   Para alterar o conjunto de permissões de um assembly para EXTERNAL_ACCESS, a permissão **EXTERNAL ACCESS ASSEMBLY** é necessária no servidor.  
  
-   Para alterar o conjunto de permissões de um assembly para UNSAFE, a permissão **UNSAFE ASSEMBLY** é necessária no servidor.  
  
-   A especificação de WITH UNCHECKED DATA, requer a permissão **ALTER ANY SCHEMA**.  


### <a name="permissions-with-clr-strict-security"></a>Permissões com a segurança estrita do CLR    
As seguintes permissões são necessárias para alterar um assembly CLR quando `CLR strict security` está habilitado:

- O usuário deve ter a permissão `ALTER ASSEMBLY`  
- Além disso, uma das seguintes condições também deve ser verdadeira:  
  - O assembly é assinado com um certificado ou uma chave assimétrica que tem um logon correspondente à permissão `UNSAFE ASSEMBLY` no servidor. A assinatura do assembly é recomendada.  
  - O banco de dados tem a propriedade `TRUSTWORTHY` definida como `ON` e o banco de dados pertence a um logon que tem a permissão `UNSAFE ASSEMBLY` no servidor. Essa opção não é recomendada.  
  
  
 Para obter mais informações sobre conjuntos de permissões de assembly, confira [Criando assemblies](../../relational-databases/clr-integration/assemblies-designing.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-refreshing-an-assembly"></a>A. Atualizando um assembly  
 O exemplo a seguir atualiza o assembly `ComplexNumber` à cópia mais recente dos módulos do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que contêm sua implementação.  
  
> [!NOTE]  
>  O assembly `ComplexNumber` pode ser criado com a execução dos scripts de exemplo UserDefinedDataType. Para obter mais informações, confira [Tipo definido pelo usuário](https://msdn.microsoft.com/library/a9b75f36-d7f5-47f7-94d6-b4448c6a2191).  
  
 ```
 ALTER ASSEMBLY ComplexNumber 
 FROM 'C:\Program Files\Microsoft SQL Server\130\Tools\Samples\1033\Engine\Programmability\CLR\UserDefinedDataType\CS\ComplexNumber\obj\Debug\ComplexNumber.dll' 
  ```

> [!IMPORTANT]
> O Banco de Dados SQL do Azure não é compatível com a referência a um arquivo.

### <a name="b-adding-a-file-to-associate-with-an-assembly"></a>B. Adicionando um arquivo a ser associado a um assembly  
 O exemplo a seguir carrega o arquivo de código fonte `Class1.cs` a ser associado ao assembly `MyClass`. Este exemplo assume que o assembly `MyClass` já foi criado no banco de dados.  
  
```  
ALTER ASSEMBLY MyClass   
ADD FILE FROM 'C:\MyClassProject\Class1.cs';  
```  

> [!IMPORTANT]
> O Banco de Dados SQL do Azure não é compatível com a referência a um arquivo.

### <a name="c-changing-the-permissions-of-an-assembly"></a>C. Alterando as permissões de um assembly  
 O exemplo a seguir altera o conjunto de permissões do assembly `ComplexNumber` de SAFE para `EXTERNAL ACCESS`.  
  
```  
ALTER ASSEMBLY ComplexNumber WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
