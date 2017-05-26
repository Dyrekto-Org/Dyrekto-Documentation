# Dyrekto-Documentation  


**1. We created pages in the backend.**  
*Creating the membership page.(Add this code)*  
```htnl
<div class="span12">
<div class="buyers-div span6 "><a href="{{store url='buyers'}}">Buyers</a></div>
<div class="sellers-div span6"><a href="{{store url='sellers'}}">Sellers</a></div>
</div>
```
*Creating the buyers page. Insert these codes and also create a file to this path for the buyers.phtml*  
```
/test/app/design/frontend/base/default/template/membership/buyers.phtml
```
>buyers.phtml
```php
<?php 
$collections = Mage::getModel('membership/group')->getCollection()->addOrder('priority','ASC');
//print_r(count($collections));exit;
/*foreach($collections as $collection)
{
echo $collection->getGroupName();
}*/
//$packages = $this->getPackages('buyer');

?>

<div class="buyer-page">
	<div class="header-nav">
		<img src="<?php echo $this->getSkinUrl('images/header-nav.png') ?>" />
		<a href="#buyer-group">Sign Up Now</a>
	</div>
	<div class="clear"></div>
	<div class="buyer-image-group">
		<ul class="products-grid">
			<li class="item">
				<div class="text">As a member, you get tons of savings and rewards to help stretch your budget</div>
				<div class="image"><img src="<?php echo $this->getSkinUrl('images/hand.png') ?>" /></div>
			</li>
			<li class="item">
				<div class="text">Plus additional benefits to boost your budget.</div>
				<div class="image"><img src="<?php echo $this->getSkinUrl('images/gift.png') ?>" /></div>
			</li>
			<li class="item last">
				<div class="text">If you haven't joined already, enroll online now to start saving money and earning points towards bigger rewards</div>
				<div class="image"><a href="#buyer-group">Sign Up Now</a><img src="<?php echo $this->getSkinUrl('images/thumb.png') ?>" /></div>
			</li>
		</ul>
	</div>
	<div class="clear"></div>
	<div class="title">Take Advantage of our vast features and services to help your profits</div>
	<div class="buyer-group" id="buyer-group">
		<ul class="products-grid">
<?php foreach($collections as $collection)
{

$pac_group_collections = Mage::getResourceModel('membership/packagegroup_collection')->addFieldToFilter('group_id', $collection->getGroupId());
$html ='';
foreach($pac_group_collections as $pac)
{
$packageModel = Mage::getModel('membership/package')->load($pac->getPackageId());
if($packageModel->getPackageId())
{
$html .='<input type="radio" name="product" required value="'.$packageModel->getProductId().'">'.$packageModel->getPackageName().' - '.Mage::helper('core')->currency($packageModel->getPackagePrice()).'<br />';
}
}
?>

<li class="item <?php echo strtolower($collection->getGroupName()) ?>">
<form action="<?php echo $this->getUrl()?>newmembership/index/post">
				<div class="buyer-type buyer-type-free"><?php echo $collection->getGroupName() ?></div>
<div class="type-desc">
<?php echo $html?>

</div>
<div class="rewardpoint">                   
<?php echo ($collection->getShippingDiscount()?'<span class="orange">'.$collection->getShippingDiscount().'</span>Discount on shipping <br/>':'') ;?>

<?php if($collection->getGroupProductPrice()){
$sprice = $collection->getGroupProductPrice();
$pos = strrpos($sprice, "%");
if ($pos) {
$sprice =  substr($sprice, 0, -1);
$disPrice = 100-(int)$sprice;
if($disPrice!=0)
$disPrice =$disPrice.'%';

}
else
{
 $disPrice = $sprice;
}

if($disPrice){

echo '<span class="orange">'.$disPrice.'</span> Discount on any purchases<br/>';
}
}?>
<?php //echo ($collection->getGroupProductPrice()?$collection->getGroupProductPrice().'Discount on any purchases<br/>':'');?> 
<?php echo ($collection->getRewardPoint()?'<span class="orange">'.$collection->getRewardPoint().'X</span> Reward Point':'');?>
</div>
<div class="special_alerts">
  <?php echo $collection->getDescription() ?>
</div>
<div class="signup-now">
  <button type="submit">Sign Up Now</button>
</div>
</form>
</li>

<?php } ?>
</ul>
	</div>
	<div class="clear"></div>
	<div class="learn-more"><a href="#"><img src="<?php echo $this->getSkinUrl('images/arrow.png') ?>" /> Learn More</a></div>
</div>
<style>

.buyer-group .signup-now button{background: #d15727;
border-radius: 5px;
color: #fff;
cursor:pointer;
padding: 8px 20px;
border: none;}
.buyer-group span.price{
color:#2f2f2f;
font-size: 14px;
font-family:Arial, Helvetica, sans-serif;
}
.bronz .buyer-type{background: #afc56f;}
.gold .buyer-type{background: #a294c1;}
.platinum .buyer-type{background: #79b9c9;}
.products-grid li.item.platinum{
margin-right: 0;
}
</style>

<script type="text/javascript">
	jQuery(document).ready(function(){
		jQuery(".products-grid input").click(function(){			
			jQuery(".products-grid  li").each(function(){
				jQuery(this).find('input[name="product"]:checked').prop("checked", false);
			})
			jQuery(this).prop("checked", true);
			console.log(jQuery(this).val());
			
		})
	})

</script>
```
Code for Buyers page in the CMS.
```html
{{block type="core/template" template="membership/buyers.phtml"}}
```
*Creating the buyers page. Insert these codes and also create a file to this path for the buyers.phtml*   
```
/test/app/design/frontend/base/default/template/membership/sellers.phtml
```
>sellers.phtml  
```php
<?php $mediaUrl	=	Mage::getBaseUrl(Mage_Core_Model_Store::URL_TYPE_MEDIA); ?>
<div class="buyer-page sellers-page">
	<div class="header-nav">
		<img src="<?php echo $this->getSkinUrl('images/sellers-header-nav.png') ?>" />
		<a href="#buyer-group">Start Selling</a>
	</div>
	<div class="title">Fastest way to Grow and Boost your Business</div>
	<div class="clear"></div>
	<div class="buyer-image-group">
		<ul class="products-grid">
			<li class="item">
				<div class="text">LARGEST CUSTOMER BASE</div>
				<div class="image"><img src="<?php echo $mediaUrl.'wysiwyg/callout/design-1.png'; ?>" /></div>
			</li>
			<li class="item">
				<div class="text">GROWTH.</div>
				<div class="image"><img src="<?php echo $mediaUrl.'wysiwyg/callout/design-2.png'; ?>" /></div>
			</li>
			<li class="item">
				<div class="text">EASE OF SELLING</div>
				<div class="image"><img src="<?php echo $mediaUrl.'wysiwyg/callout/design-3.png'; ?>" /></div>
			</li>
			<li class="item last">
				<div class="text">EXCELLENT SERVICE</div>
				<div class="image"><img src="<?php echo $mediaUrl.'wysiwyg/callout/design-4.png'; ?>" /></div>
			</li>
		</ul>
	</div>
	<div class="clear"></div>
	
	<div class="sellers-image-group buyer-image-group">
		<div class="title">Easy to list your products</div>
		<ul class="products-grid">
			<li class="item">
				<div class="image"><img src="<?php echo $mediaUrl.'wysiwyg/callout/slider-seller-1.png'; ?>" /></div>
			</li>
			<li class="item">
				<div class="image"><img src="<?php echo $mediaUrl.'wysiwyg/callout/slider-seller-2.png'; ?>" /></div>
			</li>
			<li class="item">
				<div class="image"><img src="<?php echo $mediaUrl.'wysiwyg/callout/slider-seller-3.png'; ?>" /></div>
			</li>
			<li class="item last">
				<div class="image"><img src="<?php echo $mediaUrl.'wysiwyg/callout/slider-seller-4.png'; ?>" /></div>
			</li>
		</ul>
		<div class="clear"></div>
	</div>
	<div class="clear"></div>
	<div class="title">Take Advantage of our waste features and services to help your profits</div>
	<div class="buyer-group" id="buyer-group">
		<ul class="products-grid">
			<li class="item">
<form action="<?php echo $this->getUrl()?>newmembership/index/sellerpost">
				<div class="buyer-type buyer-type-free">STARTER</div>
				<div class="type-desc">

					<!--<strong>Selling 20 items/$5000</strong><br/>-->
<?php $glodpackages = $this->getFilterPackages('seller','starter') ;

$titleRow = $glodpackages->getFirstItem();
//print_r($titleRow);
if( $titleRow->getTitle())
{
	echo '<strong>'.$titleRow->getTitle().'</strong><br/>';
}
foreach($glodpackages as $package){
?>
<input type="radio" name="product" required value="<?php echo $package->getProductId()?>">
<?php   echo $package->getPackageName().' - '.Mage::helper('core')->currency($package->getPackagePrice()).'<br />'; } ?>
</div>
				<div class="rewardpoint">
					<?php echo $package->getDescription()?>
				</div>
				<div class="signup-now">
					<button type="submit">Start Selling</button>
				</div>
</form>
			</li>
			<li class="item">
<form action="<?php echo $this->getUrl()?>newmembership/index/sellerpost">
				<div class="buyer-type buyer-type-bronz">SMALL BUSINESS</div>
				<div class="type-desc">
					<!--<strong>Selling 100 items/$30000</strong><br/>-->

<?php $glodpackages = $this->getFilterPackages('seller','small_buisness') ;
$titleRow = $glodpackages->getFirstItem();
//print_r($titleRow);
if( $titleRow->getTitle())
{
	echo '<strong>'.$titleRow->getTitle().'</strong><br/>';
	
}
foreach($glodpackages as $package) { ?>
<input type="radio" name="product" required value="<?php echo $package->getProductId()?>">
<?php   echo $package->getPackageName().' - '.Mage::helper('core')->currency($package->getPackagePrice()).'<br />'; } ?>
	</div>
				<div class="rewardpoint">
					<?php echo $package->getDescription()?>
				</div>
				<div class="signup-now">
					<button type="submit">Start Selling</button>
</div>
</form>
			</li>
<li class="item">
  <form action="<?php echo $this->getUrl()?>newmembership/index/sellerpost">
  <div class="buyer-type buyer-type-gold">PROFFESIONAL</div>
  <div class="type-desc">
					
<!--<strong>Selling 500 items/$200000</strong><br/>-->
<?php $glodpackages = $this->getFilterPackages('seller','professional') ;
$titleRow = $glodpackages->getFirstItem();
//print_r($titleRow);
if( $titleRow->getTitle())
{
	echo '<strong>'.$titleRow->getTitle().'</strong><br/>';
}
foreach($glodpackages as $package){
?>
<input type="radio" name="product" required value="<?php echo $package->getProductId()?>">
<?php   echo $package->getPackageName().' - '.Mage::helper('core')->currency($package->getPackagePrice()).'<br />';
                                             
}
?>
				</div>
				<div class="rewardpoint">
					<?php echo $package->getDescription()?>
				</div>
				<div class="signup-now">
					<button type="submit">Start Selling</button>
				</div>
</form>
</li>
<li class="item last">
<form action="<?php echo $this->getUrl()?>newmembership/index/sellerpost">
				<div class="buyer-type buyer-type-platinum">ENTERPRISE</div>
				<div class="type-desc">
					<!--<strong>Unlimited</strong><br/>-->
					<?php $glodpackages = $this->getFilterPackages('seller','enterprize') ;
					$titleRow = $glodpackages->getFirstItem();
//print_r($titleRow);
if( $titleRow->getTitle())
{
	echo '<strong>'.$titleRow->getTitle().'</strong><br/>';
}
foreach($glodpackages as $package){
?>
<input type="radio" name="product" required value="<?php echo $package->getProductId()?>">
<?php   echo $package->getPackageName().' - '.Mage::helper('core')->currency($package->getPackagePrice()).'<br />';
 }
?>
					<div class="clear"></div>
				</div>
				<div class="rewardpoint">
					<?php echo $package->getDescription()?>
				</div>
				<div class="signup-now">
					<button type="submit">Start Selling</button>
				</div>
</form>
			</li>
		</ul>
	</div>
	<div class="clear"></div>
	<div class="learn-more"><a href="#"><img src="<?php echo $this->getSkinUrl('images/arrow.png') ?>" /> Learn More</a></div>
</div>
<style>

.buyer-group .signup-now button{background: #d15727;
border-radius: 5px;
color: #fff;
cursor:pointer;
padding: 8px 20px;
border: none;}
.buyer-group span.price{
color:#2f2f2f;
font-size: 14px;
font-family:Arial, Helvetica, sans-serif;
}
</style>
<script type="text/javascript">
	jQuery(document).ready(function(){
		jQuery(".products-grid input").click(function(){			
			jQuery(".products-grid  li").each(function(){
				jQuery(this).find('input[name="product"]:checked').prop("checked", false);
			})
			jQuery(this).prop("checked", true);
			console.log(jQuery(this).val());
			
		})
	})

</script>

```
Code for Sellers page in the CMS.
```html
{{block type="core/template" template="membership/sellers.phtml"}}
```
