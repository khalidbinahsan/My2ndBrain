To active the elementor pro dowonload it from Hustlewp and then make this modification. Go to Elementor Pro > lisence > api.php then find the function get_license_data and replace with the following code
```php
public static function get_license_data( $force_request = false ) {
		return [
			'success'          => true,
			'license'          => 'valid',
			'payment_id'       => '1001',
			'license_limit'    => '100',
			'site_count'       => '1',
			'activations_left' => '99',
			'expires'          => '2070-01-01 00:00:00',
			'membership_id'    => '123',
			'tier'             => self::TIER_AGENCY,
			'generation'       => 'essential-oct2023',
			'recurring'        => false,
			'features'         => [
				'pro_trial',
				'template_access_level_3',
				'widget_access_level_3',
			],
		];
	}
```