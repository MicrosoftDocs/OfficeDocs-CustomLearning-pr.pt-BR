---
author: pkrebs
ms.author: pkrebs
title: Atualização de aprendizagem personalizada
ms.date: 02/10/2019
description: Aprendizagem personalizada para a configuração da Web Part manual do Office 365
ms.openlocfilehash: f9729c922b374cc6b775737fa7c7c76a4719534c
ms.sourcegitcommit: b6617bbbaee0784d6216e96052c2469f97cf51e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2019
ms.locfileid: "30411891"
---
# <a name="manual-upgrade-for-custom-learning"></a><span data-ttu-id="22e26-103">Atualização manual para aprendizagem personalizada</span><span class="sxs-lookup"><span data-stu-id="22e26-103">Manual Upgrade for Custom Learning</span></span>

<span data-ttu-id="22e26-104">O aprendizado personalizado para o Office 365 fornece um processo de atualização manual para organizações que participaram de pilotos mais antigos.</span><span class="sxs-lookup"><span data-stu-id="22e26-104">Custom Learning for Office 365 provides a manual upgrade process for organizations that have participated in earlier pilots.</span></span> <span data-ttu-id="22e26-105">Com o processo de atualização, as organizações podem continuar a usar seu site de aprendizado personalizado atual e atualizar adicionando a nova Web Part de aprendizado personalizado aprimorada ao seu catálogo de aplicativos do SharePoint e, em seguida, executando um script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22e26-105">With the upgrade process, organizations can continue to use their current Custom Learning site and upgrade by adding the new, enhanced Custom Learning web part to their SharePoint App Catalog, and then running a PowerShell script.</span></span> <span data-ttu-id="22e26-106">O seguinte fornece uma visão geral do processo de atualização:</span><span class="sxs-lookup"><span data-stu-id="22e26-106">The following provides an overview of the upgrade process:</span></span> 

- <span data-ttu-id="22e26-107">Validar que a pessoa responsável por carregar a nova Web Part e executar o script do PowerShell tem as permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="22e26-107">Validate that the person responsible for uploading the new web part and running the Powershell script has the required permissions</span></span>
- <span data-ttu-id="22e26-108">Carregue a Web Part, o arquivo customlearning. sppkg, para o catálogo de aplicativos do locatário do Office 365</span><span class="sxs-lookup"><span data-stu-id="22e26-108">Upload the web part, customlearning.sppkg file, to your Office 365 Tenant App Catalog</span></span>
- <span data-ttu-id="22e26-109">Executar um script do PowerShell que irá configurar seu locatário com os artefatos apropriados necessários para o aprendizado personalizado</span><span class="sxs-lookup"><span data-stu-id="22e26-109">Execute a PowerShell script that will configure your tenant with the appropriate artifacts required for Custom Learning</span></span>
- <span data-ttu-id="22e26-110">Navegue até a página CustomLearningAdmin. aspx no site de aprendizado personalizado para inicializar a configuração personalizada do ccontent.</span><span class="sxs-lookup"><span data-stu-id="22e26-110">Navigate to the CustomLearningAdmin.aspx page in the Custom Learning site to to initialize the Custom Ccontent configuration.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22e26-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="22e26-111">Prerequisites</span></span>
<span data-ttu-id="22e26-112">Para garantir uma atualização bem-sucedida do aprendizado personalizado, os pré-requisitos a seguir devem ser atendidos.</span><span class="sxs-lookup"><span data-stu-id="22e26-112">To ensure a successful upgrade of Custom Learning, the following prerequisites must be met.</span></span> 

- <span data-ttu-id="22e26-113">Você deve ter configurado um catálogo de aplicativos em todo o locatário.</span><span class="sxs-lookup"><span data-stu-id="22e26-113">You must have set up a tenant-wide App Catalog.</span></span> <span data-ttu-id="22e26-114">Se você não tiver um catálogo de aplicativos de locatário, confira [Configurar o locatário do Office 365](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-developer-tenant#create-app-catalog-site) e siga a seção criar site de catálogo de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="22e26-114">If you don't have a Tenant App Catalog, please see [Set up your Office 365 tenant](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-developer-tenant#create-app-catalog-site) and follow the Create app catalog site section.</span></span> 
- <span data-ttu-id="22e26-115">Se o catálogo de aplicativos de todo o locatário já tiver sido provisionado, você precisará ter acesso a uma conta que tenha direitos para carregar um pacote nele.</span><span class="sxs-lookup"><span data-stu-id="22e26-115">If your tenant-wide App Catalog has already been provisioned, you need access to an account that has rights to upload a package to it.</span></span> <span data-ttu-id="22e26-116">Geralmente, esta é uma conta com a função de administrador do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="22e26-116">Generally this is an account with the SharePoint Administrator role.</span></span> 
- <span data-ttu-id="22e26-117">Se uma conta com a função de administrador do SharePoint não funcionar: Vá para o centro de administração do SharePoint, selecione o catálogo de aplicativos, clique em proprietários e entre como um dos administradores de conjunto de sites ou adicione a conta de administrador do SharePoint que falhou ao site Lista de administradores de coleção.</span><span class="sxs-lookup"><span data-stu-id="22e26-117">If an account with the SharePoint Administrator's role doesn't work: Go to the SharePoint Admin Center, select the App Catalog, click Owners, and sign in as one of the Site Collection Administrators or add the SharePoint Administrator account that failed to the Site Collection Administrators list.</span></span> 

## <a name="step-1---get-the-web-part-package-and-setup-script-from-github"></a><span data-ttu-id="22e26-118">Etapa 1: obter o pacote de Web Part e o script de instalação do GitHub</span><span class="sxs-lookup"><span data-stu-id="22e26-118">Step 1 - Get the web part package and setup script from GitHub</span></span>
<span data-ttu-id="22e26-119">Como parte do processo de instalação, você precisará do pacote de Web Part de aprendizado personalizado e do script de instalação do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22e26-119">As part of the setup process, you'll need the Custom Learning Web part package and the PowerShell Setup Script.</span></span>

1. <span data-ttu-id="22e26-120">Vá para o [repositório do GitHub de aprendizado personalizado](https://github.com/pnp/custom-learning-office-365).</span><span class="sxs-lookup"><span data-stu-id="22e26-120">Go the the [Custom Learning GitHub Repository](https://github.com/pnp/custom-learning-office-365).</span></span>
2. <span data-ttu-id="22e26-121">Clique em **clonar ou baixar**e, em seguida, **Baixe zip**.</span><span class="sxs-lookup"><span data-stu-id="22e26-121">Click **Clone or download**, and then **Download ZIP**.</span></span>   
3. <span data-ttu-id="22e26-122">Salve o arquivo **zip** em um local na sua unidade local.</span><span class="sxs-lookup"><span data-stu-id="22e26-122">Save the **ZIP** file to a location on your local drive.</span></span>
4. <span data-ttu-id="22e26-123">Extraia o arquivo **zip** em sua unidade local.</span><span class="sxs-lookup"><span data-stu-id="22e26-123">Extract the **ZIP** file on your local drive.</span></span>

## <a name="step-2---upload-the-web-part-to-the-tenant-app-catalog"></a><span data-ttu-id="22e26-124">Etapa 2-carregar a Web Part no catálogo de aplicativos do locatário</span><span class="sxs-lookup"><span data-stu-id="22e26-124">Step 2 - Upload the web part to the Tenant App Catalog</span></span>
<span data-ttu-id="22e26-125">Para configurar o aprendizado personalizado para o Office 365, você carrega o arquivo customlearning. sppkg no catálogo de aplicativos de todo o locatário e o implanta.</span><span class="sxs-lookup"><span data-stu-id="22e26-125">To set up Custom Learning for Office 365, you upload the customlearning.sppkg file to the tenant-wide App Catalog and deploy it.</span></span> <span data-ttu-id="22e26-126">Consulte [usar o catálogo de aplicativos para disponibilizar aplicativos de negócios personalizados para seu ambiente do SharePoint Online](https://docs.microsoft.com/en-us/sharepoint/use-app-catalog) para obter instruções detalhadas sobre como adicionar um aplicativo ao catálogo de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="22e26-126">Please see [Use the App Catalog to make custom business apps available for your SharePoint Online environment](https://docs.microsoft.com/en-us/sharepoint/use-app-catalog) for detailed instructions on how to add an app to the app catalog.</span></span>

1. <span data-ttu-id="22e26-127">No Office 365, clique em **administrador**.</span><span class="sxs-lookup"><span data-stu-id="22e26-127">In Office 365, click **Admin**.</span></span>
2. <span data-ttu-id="22e26-128">Em **centros de administração**, clique em **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="22e26-128">Under **Admin centers**, click **SharePoint**.</span></span>
3. <span data-ttu-id="22e26-129"> > Clique \*\*\*\* em*\*Catálogo** > *\*de aplicativos do aplicativo distribua aplicativos para SharePoint.**</span><span class="sxs-lookup"><span data-stu-id="22e26-129">Click **apps** > **App Catalog** > **Distribute apps for SharePoint.**</span></span>
4. <span data-ttu-id="22e26-130">Clique em **carregar** > **escolher arquivos**.</span><span class="sxs-lookup"><span data-stu-id="22e26-130">Click **Upload** > **Choose Files**.</span></span>
5. <span data-ttu-id="22e26-131">Na pasta onde você salvou o arquivo ZIP, selecione a pasta **WebPart** e, em seguida, selecione **customlearning. sppkg.**</span><span class="sxs-lookup"><span data-stu-id="22e26-131">In the folder where you saved the ZIP file, select the **webpart** folder, and then select **customlearning.sppkg.**</span></span>
6. <span data-ttu-id="22e26-132">Clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="22e26-132">Click **Deploy**.</span></span>

## <a name="step-5--execute-powershell-configuration-script"></a><span data-ttu-id="22e26-133">Etapa 5: executar o script de configuração do PowerShell</span><span class="sxs-lookup"><span data-stu-id="22e26-133">Step 5- Execute PowerShell Configuration Script</span></span>
<span data-ttu-id="22e26-134">Um script `CustomLearningConfiguration.ps1` do PowerShell está incluído no download do zip no github.</span><span class="sxs-lookup"><span data-stu-id="22e26-134">A PowerShell script `CustomLearningConfiguration.ps1` is included in the ZIP download from GitHub.</span></span> <span data-ttu-id="22e26-135">Você precisa executar o script para criar três [Propriedades de locatário](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/tenant-properties) que a solução usa.</span><span class="sxs-lookup"><span data-stu-id="22e26-135">You need to execute the script to create three [tenant properties](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/tenant-properties) that the solution uses.</span></span> <span data-ttu-id="22e26-136">Além disso, o script cria duas [páginas de aplicativo de parte única](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/single-part-app-pages) na biblioteca de páginas do site para hospedar as Web Parts de administrador e usuário em um local conhecido.</span><span class="sxs-lookup"><span data-stu-id="22e26-136">In addition, the script creates two [single part app pages](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/single-part-app-pages) in the site pages library to host the admin and user web parts at a known location.</span></span> <span data-ttu-id="22e26-137">Essas páginas de aplicativos são:</span><span class="sxs-lookup"><span data-stu-id="22e26-137">These app pages are:</span></span>

- <span data-ttu-id="22e26-138">CustomAdministration. aspx</span><span class="sxs-lookup"><span data-stu-id="22e26-138">CustomAdministration.aspx</span></span>
- <span data-ttu-id="22e26-139">CustomViewer. aspx</span><span class="sxs-lookup"><span data-stu-id="22e26-139">CustomViewer.aspx</span></span>

### <a name="to-run-the-powershell-script"></a><span data-ttu-id="22e26-140">Para executar o script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="22e26-140">To run the Powershell Script</span></span>
- <span data-ttu-id="22e26-141">Usando o PowerShell, execute `CustomLearningConfiguration.ps1` o script localizado na pasta WEBPART do zip do github.</span><span class="sxs-lookup"><span data-stu-id="22e26-141">Using PowerShell, execute the `CustomLearningConfiguration.ps1` script located in the webpart folder from the GitHub ZIP.</span></span> <span data-ttu-id="22e26-142">Se tiver êxito, você verá três pares chave/valor e **administrador de aprendizado personalizado para desativar...** na janela de comando.</span><span class="sxs-lookup"><span data-stu-id="22e26-142">If successful, you'll see three key/value pairs and **Custom Learning Admin for Off...** in the Command window.</span></span>

### <a name="disabling-telemetry-collection"></a><span data-ttu-id="22e26-143">Desabilitando a coleção de teleMetria</span><span class="sxs-lookup"><span data-stu-id="22e26-143">Disabling Telemetry Collection</span></span>
<span data-ttu-id="22e26-144">O aprendizado personalizado inclui consentimento de controle de telemetria anônimo, que por padrão é definido como ativado.</span><span class="sxs-lookup"><span data-stu-id="22e26-144">Custom Learning includes anonymized telemetry tracking opt in, which by default is set to on.</span></span> <span data-ttu-id="22e26-145">Se quiser desativar o rastreamento de telemetria, altere o `CustomlearningConfiguration.ps1` script para definir a `$optInTelemetry` variável como. `$false`</span><span class="sxs-lookup"><span data-stu-id="22e26-145">If you  would like to turn telemetry tracking off, please change the `CustomlearningConfiguration.ps1` script to set the `$optInTelemetry` variable to `$false`.</span></span>

## <a name="step-6---initialize-web-part-custom-configuration"></a><span data-ttu-id="22e26-146">Etapa 6-inicializar a configuração personalizada da Web Part</span><span class="sxs-lookup"><span data-stu-id="22e26-146">Step 6 - Initialize web part custom configuration</span></span>
<span data-ttu-id="22e26-147">Após o script do PowerShell ser executado com êxito, navegue `<YOUR-SITE-COLLECTION-URL>/SitePages/CustomLearningAdmin.aspx`até.</span><span class="sxs-lookup"><span data-stu-id="22e26-147">After the PowerShell script is successfully run, navigate to `<YOUR-SITE-COLLECTION-URL>/SitePages/CustomLearningAdmin.aspx`.</span></span> <span data-ttu-id="22e26-148">Abrir **CustomLearningAdmin. aspx** Inicializa o item de lista **CustomConfig** que configura o aprendizado personalizado para o primeiro uso.</span><span class="sxs-lookup"><span data-stu-id="22e26-148">Opening **CustomLearningAdmin.aspx** initializes the **CustomConfig** list item that sets up Custom Learning for first use.</span></span> <span data-ttu-id="22e26-149">Você verá uma página parecida com esta:</span><span class="sxs-lookup"><span data-stu-id="22e26-149">You should see a page that looks like this:</span></span>

![CG-adminapppage. png](media/cg-adminapppage.png)

## <a name="add-owners-to-site"></a><span data-ttu-id="22e26-151">Adicionar proprietários ao site</span><span class="sxs-lookup"><span data-stu-id="22e26-151">Add Owners to Site</span></span>
<span data-ttu-id="22e26-152">Como administrador de locatários, é improvável que você seja a pessoa que personaliza o site, portanto, você precisará atribuir alguns proprietários ao site.</span><span class="sxs-lookup"><span data-stu-id="22e26-152">As the Tenant Admin, it's unlikely you'll be the person customizing the site, so you'll need to assign a few owners to the site.</span></span> <span data-ttu-id="22e26-153">Os proprietários têm privilégios administrativos no site para que eles possam modificar as páginas do site e remarcar o site.</span><span class="sxs-lookup"><span data-stu-id="22e26-153">Owners have administrative privileges on the site so they can modify site pages and rebrand the site.</span></span> <span data-ttu-id="22e26-154">Eles também podem ocultar e mostrar o conteúdo fornecido por meio da Web Part de aprendizado personalizado.</span><span class="sxs-lookup"><span data-stu-id="22e26-154">They also have the ability to hide and show content delivered through the Custom Learning Web part.</span></span> <span data-ttu-id="22e26-155">Eles também terão a capacidade de criar uma lista de reprodução personalizada e atribuí-las às subcategorias personalizadas.</span><span class="sxs-lookup"><span data-stu-id="22e26-155">They'll also have the ability to build custom playlist and assign them to custom subcategories.</span></span>  

1. <span data-ttu-id="22e26-156">No menu **configurações** do SharePoint, clique em **permissões do site**.</span><span class="sxs-lookup"><span data-stu-id="22e26-156">From the SharePoint **Settings** menu, click **Site Permissions**.</span></span>
2. <span data-ttu-id="22e26-157">Clique em **configurações de permissão avançadas**.</span><span class="sxs-lookup"><span data-stu-id="22e26-157">Click **Advanced Permission Settings**.</span></span>
3. <span data-ttu-id="22e26-158">Clique em **aprendizagem personalizada para proprietários do Office 365**.</span><span class="sxs-lookup"><span data-stu-id="22e26-158">Click **Custom learning for Office 365 Owners**.</span></span>
4. <span data-ttu-id="22e26-159">Clique em **novo** > **Adicionar usuários a este grupo**, adicione as pessoas que você deseja que sejam proprietários e clique em **compartilhar**.</span><span class="sxs-lookup"><span data-stu-id="22e26-159">Click **New** > **Add Users to this group**, add the people you want to be Owners, and then click **Share**.</span></span>

<span data-ttu-id="22e26-160">A atualização já está concluída.</span><span class="sxs-lookup"><span data-stu-id="22e26-160">The upgrade is now complete.</span></span> <span data-ttu-id="22e26-161">Para saber mais sobre como personalizar o site de aprendizado personalizado e a Web Part para seu ambiente, consulte [Customize The Training Experience](custom_overview.md).</span><span class="sxs-lookup"><span data-stu-id="22e26-161">To learn more about how to tailor the Custom Learning site and web part for your environment, see [Customize the training experience](custom_overview.md).</span></span>

## <a name="upgrade-instructions-for-site-owners"></a><span data-ttu-id="22e26-162">Instruções de atualização para proprietários de site</span><span class="sxs-lookup"><span data-stu-id="22e26-162">Upgrade Instructions for Site Owners</span></span>
<span data-ttu-id="22e26-163">O aprendizado personalizado para o Office 365 introduziu uma variedade de aprimoramentos na Web Part.</span><span class="sxs-lookup"><span data-stu-id="22e26-163">Custom Learning for office 365 has introduced a variety of enhancements to the web part.</span></span> <span data-ttu-id="22e26-164">Trabalhar com a Web Part é abordado em detalhes na seção [Personalizar a experiência de aprendizagem](custom_overview.md) .</span><span class="sxs-lookup"><span data-stu-id="22e26-164">Working with the web part is covered in detail in the [Customize the learning experience](custom_overview.md) section.</span></span> <span data-ttu-id="22e26-165">Por enquanto, o proprietário do site deve:</span><span class="sxs-lookup"><span data-stu-id="22e26-165">For now, the Site Owner should:</span></span>  

- <span data-ttu-id="22e26-166">Verifique se a Web Part de aprendizagem personalizada para Office 365 está disponível.</span><span class="sxs-lookup"><span data-stu-id="22e26-166">Verify the Custom Learning for Office 365 Web part is available.</span></span> 
- <span data-ttu-id="22e26-167">Substituir a Web Part existente em páginas com a nova Web Part</span><span class="sxs-lookup"><span data-stu-id="22e26-167">Replace the existing web part on pages with the new web part</span></span>
- <span data-ttu-id="22e26-168">Substitua os links que apontam para a Web Part antiga</span><span class="sxs-lookup"><span data-stu-id="22e26-168">Replace any links pointing to the old web part</span></span>

### <a name="verify-the-custom-learning-for-office-365-web-part-is-available"></a><span data-ttu-id="22e26-169">Verifique se a Web Part de aprendizagem personalizada para Office 365 está disponível</span><span class="sxs-lookup"><span data-stu-id="22e26-169">Verify the Custom Learning for Office 365 web part is available</span></span>
1.  <span data-ttu-id="22e26-170">No site de aprendizado personalizado, clique em **configurações**e, em seguida, clique em \***Adicionar uma página**.</span><span class="sxs-lookup"><span data-stu-id="22e26-170">From the Custom Learning site, click **Settings**, and then click \***Add a Page**.</span></span>
2.  <span data-ttu-id="22e26-171">Clique no **+** ícone da página para adicionar uma Web Part e selecione a Web Part **aprendizado personalizado para o Office 365** .</span><span class="sxs-lookup"><span data-stu-id="22e26-171">Click the **+** icon on the page to add a web part, and then select the **Custom Learning for Office 365** web part.</span></span> <span data-ttu-id="22e26-172">A página agora deve ser semelhante ao seguinte gráfico:</span><span class="sxs-lookup"><span data-stu-id="22e26-172">The page should now look similar to the following graphic:</span></span>

[<span data-ttu-id="22e26-173">CG-adminapppage. png</span><span class="sxs-lookup"><span data-stu-id="22e26-173">cg-adminapppage.png</span></span>](media/cg-adminapppage.png)
 
### <a name="replace-the-old-web-part-with-the-new-web-part"></a><span data-ttu-id="22e26-174">Substituir a Web Part antiga pela Web Part nova</span><span class="sxs-lookup"><span data-stu-id="22e26-174">Replace the old web part with the new web part</span></span>
<span data-ttu-id="22e26-175">Antes de substituir a Web Part de aprendizado personalizada ou fazer alterações no site, recomendamos que você leia a documentação [Personalizar a experiência de aprendizagem](custom_overview.md) , conforme explica como usar a nova Web Part.</span><span class="sxs-lookup"><span data-stu-id="22e26-175">Before replacing the Custom Learning web part or making changes to the site, we recommend you read the [Customize the Learning Experience](custom_overview.md) documentation as it explains how to use the new web part.</span></span> 

<span data-ttu-id="22e26-176">Para atualizar o site de aprendizado personalizado, substitua as instâncias existentes da Web Part pela nova Web Part.</span><span class="sxs-lookup"><span data-stu-id="22e26-176">To upgrade the Custom Learning site, replace existing instances of the Web part with the new Web part.</span></span> <span data-ttu-id="22e26-177">Embora não possamos ter certeza de onde a Web Part foi adicionada, a orientação para os pilotos anteriores era adicionar a Web Part às seguintes páginas, portanto, procure substituir a Web Part nessas páginas:</span><span class="sxs-lookup"><span data-stu-id="22e26-177">While we can’t be sure where the Web part has been added, the guidance for previous pilots was to add the web part to the following pages, so look to replace the web part on these pages:</span></span>

- <span data-ttu-id="22e26-178">Get-started-with-Office-365. aspx</span><span class="sxs-lookup"><span data-stu-id="22e26-178">Get-started-with-Office-365.aspx</span></span>
- <span data-ttu-id="22e26-179">Get-started-with-Microsoft-Teams. aspx</span><span class="sxs-lookup"><span data-stu-id="22e26-179">Get-started-with-Microsoft-Teams.aspx</span></span>
- <span data-ttu-id="22e26-180">Get-started-with-OneDrive. aspx</span><span class="sxs-lookup"><span data-stu-id="22e26-180">Get-started-with-OneDrive.aspx</span></span>
- <span data-ttu-id="22e26-181">Get-started-with-SharePoint. aspx</span><span class="sxs-lookup"><span data-stu-id="22e26-181">Get-started-with-SharePoint.aspx</span></span>

### <a name="replace-existing-links-to-the-web-part"></a><span data-ttu-id="22e26-182">Substituir links existentes à Web Part</span><span class="sxs-lookup"><span data-stu-id="22e26-182">Replace existing links to the web part</span></span>
<span data-ttu-id="22e26-183">Com os aprimoramentos da nova Web Part, a forma de vincular a uma lista de reprodução foi alterada.</span><span class="sxs-lookup"><span data-stu-id="22e26-183">With the enhancements to the new web part, they way that you link to a playlist has changed.</span></span> <span data-ttu-id="22e26-184">Como parte da atualização, você deve substituir todos os links para a Web Part, incluindo itens de menu e links na página inicial.</span><span class="sxs-lookup"><span data-stu-id="22e26-184">As part of the upgrade, you should replace any links to the web part, including menu items, and links on the Home page.</span></span> <span data-ttu-id="22e26-185">Antes de substituir a Web Part de aprendizado personalizada ou fazer alterações no site, recomendamos que você leia a documentação [Personalizar a experiência de aprendizagem](custom_overview.md) , conforme explica como usar a nova Web Part.</span><span class="sxs-lookup"><span data-stu-id="22e26-185">Before replacing the Custom Learning web part or making changes to the site, we recommend you read the [Customize the Learning Experience](custom_overview.md) documentation as it explains how to use the new web part.</span></span> 

## <a name="recreate-existing-playlists"></a><span data-ttu-id="22e26-186">Recriar playlists existentes</span><span class="sxs-lookup"><span data-stu-id="22e26-186">Recreate existing playlists</span></span> 
<span data-ttu-id="22e26-187">Para garantir que as listas de reprodução funcionem corretamente, qualquer lista de reprodução que tenha sido criada com a versão anterior da Web Part precisará ser recriada.</span><span class="sxs-lookup"><span data-stu-id="22e26-187">To ensure that playlists work properly, any playlists that have been created with the earlier version of the web part will need to be recreated.</span></span> <span data-ttu-id="22e26-188">Antes de excluir as listas de reprodução, faça uma lista das listas de reprodução e dos ativos associados para que você possa recriá-las facilmente com a nova Web Part de aprendizado personalizado.</span><span class="sxs-lookup"><span data-stu-id="22e26-188">Before deleting the playlists, make a list of the custom playlists and associated assets so you can recreate them easily with the new Custom Learning Web part.</span></span> <span data-ttu-id="22e26-189">Faça uma cópia de uma lista de reprodução e, em seguida, exclua-a.</span><span class="sxs-lookup"><span data-stu-id="22e26-189">Make a copy of a playlist and then delete it.</span></span> <span data-ttu-id="22e26-190">Você pode usar o campo JSONData para fazer uma cópia do conteúdo de uma lista de reprodução antes de excluir.</span><span class="sxs-lookup"><span data-stu-id="22e26-190">You can use the JSONData field to make a copy of the content of a playlist before you delete.</span></span> <span data-ttu-id="22e26-191">Isso facilitará a criação mais tarde.</span><span class="sxs-lookup"><span data-stu-id="22e26-191">This will make it easier to create later.</span></span>


<span data-ttu-id="22e26-192">• No site de aprendizado personalizado, clique em configurações > conteúdo do site.</span><span class="sxs-lookup"><span data-stu-id="22e26-192">•   From the Custom Learning site, click Settings > Site Content.</span></span> <span data-ttu-id="22e26-193">• Selecione uma lista de reprodução, selecione as reticências, selecione Editar e copie o conteúdo do campo JSONData e salve no bloco de notas ou em um documento separado para referência posterior.</span><span class="sxs-lookup"><span data-stu-id="22e26-193">•   Select a playlist, select the ellipses, select Edit, and then copy the contents of the JSONData field and save in NotePad or a separate document for later reference.</span></span> <span data-ttu-id="22e26-194">Selecione cancelar.</span><span class="sxs-lookup"><span data-stu-id="22e26-194">Select Cancel.</span></span>
<span data-ttu-id="22e26-195">• Selecione a lista de reprodução, selecione as reticências e, em seguida, selecione Excluir.</span><span class="sxs-lookup"><span data-stu-id="22e26-195">•   Select the playlist, select the ellipses, and then select Delete.</span></span>
<span data-ttu-id="22e26-196">• Agora você está pronto para recriar a lista de reprodução com a nova Web Part.</span><span class="sxs-lookup"><span data-stu-id="22e26-196">•   You are now ready to recreate the playlist with the new Web part.</span></span>
<span data-ttu-id="22e26-197">Para obter instruções sobre como usar a nova Web Part de aprendizagem personalizada para o https://docs.microsoft.com/en-us/office365/customlearning/custom_overviewOffice 365, consulte.</span><span class="sxs-lookup"><span data-stu-id="22e26-197">For instructions on using the new Custom Learning for Office 365 Web part, see https://docs.microsoft.com/en-us/office365/customlearning/custom_overview.</span></span>

## <a name="step-8---chan"></a><span data-ttu-id="22e26-198">Etapa 8-canal</span><span class="sxs-lookup"><span data-stu-id="22e26-198">Step 8 - Chan</span></span>

### <a name="next-steps"></a><span data-ttu-id="22e26-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="22e26-199">Next Steps</span></span>
- <span data-ttu-id="22e26-200">[Personalizar](custom_overview.md) a experiência de treinamento da sua organização.</span><span class="sxs-lookup"><span data-stu-id="22e26-200">[Customize](custom_overview.md) the training experience for your organization.</span></span>
