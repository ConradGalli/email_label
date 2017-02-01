# email_label


$tracking_number   = get_post_meta( $order_id, '_tracking_number', true );
						$date_shipped      = get_post_meta( $order_id, '_date_shipped', true );
	 					$date_shipped = ' ' . sprintf( __( 'on %s', 'wc_shipment_tracking' ), date_i18n( __( 'l jS F Y', 'wc_shipment_tracking'), $date_shipped ) );
						$link = 'https://tools.usps.com/go/TrackConfirmAction_input?qtc_tLabels1='. $tracking_number; 
	 					$tracking_link = sprintf( __('Click here to track your shipment', 'wc_shipment_tracking') . ': <a href="%s">%s</a>', $link, $link );
					
						$tracking_provider = ' ' . __('via', 'wc_shipment_tracking') . ' <strong>USPS</strong>';
						$message_body = wpautop( sprintf( __('Your order was shipped%s%s. Tracking number %s. %s', 'wc_shipment_tracking'), $date_shipped, $tracking_provider, $tracking_number, $tracking_link ) );
						$mailer = $woocommerce->mailer();
						$message = $mailer->wrap_message(sprintf( __( 'Order %s shipped' ), $orders->get_order_number() ), $message_body );
						$mailer->send( $orders->billing_email, sprintf( __( 'Order %s shipped' ), $orders->get_order_number() ), $message );
