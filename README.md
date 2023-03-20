# sandbox

# Inleiding

## Introductie

### Form customizer
Vanaf versie 1.10.0.0 is het formulieren component uitgebreid met een form customizer-extensie. Hiermee kan het gedrag van de Sharepoint-lijst (New, Edit, Display) gecontroleerd worden zodat de SharePoint lijst-functionaliteit Nieuw, Bewerken en Weergave gebruikt kan worden in combinatie met het formulieren component. De form customizer moet met Powershell gekoppeld worden aan het betreffende content type.

```Powershell
connect-pnponline -Url $siteurl -Interactive #-Credentials $creds
$componentId = "5a7d3291-7ceb-4e77-b5f0-25ef52e010e4"
$formurl = "<absolute-url-to-page-with-form-component>"
$props = @{
    "form" = $formurl #"https://devrico.sharepoint.com/sites/formOfferteAanvragen/SitePages/Formulier.aspx"
} | ConvertTo-Json

$contentType = Get-PnPContentType -Identity "Demo"
$contentType.DisplayFormClientSideComponentId = $componentId
$contentType.DisplayFormClientSideComponentProperties = $props

$contentType.NewFormClientSideComponentId = $componentId 
$contentType.NewFormClientSideComponentProperties = $props

$contentType.EditFormClientSideComponentId = $componentId
$contentType.EditFormClientSideComponentProperties = $props
$contentType.Update($true)
```
